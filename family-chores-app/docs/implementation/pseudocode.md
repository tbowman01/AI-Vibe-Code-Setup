# Pseudocode with TDD Anchors

This document provides modular pseudocode for key features of the Family Chores Application, including minimal TDD anchors to guide the next steps in development.

## Module: User Authentication

### 1. User Registration (Email)

```pseudocode
// TDD Anchor: Test_UserRegistration_WithValidEmailAndPassword_CreatesUser
// TDD Anchor: Test_UserRegistration_WithExistingEmail_ReturnsError
// TDD Anchor: Test_UserRegistration_WithInvalidPassword_ReturnsError

FUNCTION registerUserWithEmail(email, password)
  // Input validation
  IF NOT isValidEmail(email) THEN
    RETURN error "Invalid email format"
  ENDIF
  IF NOT isStrongPassword(password) THEN
    RETURN error "Password does not meet complexity requirements"
  ENDIF

  // Check if user already exists
  existingUser = Database.findUserByEmail(email)
  IF existingUser IS NOT NULL THEN
    RETURN error "Email already registered"
  ENDIF

  // Hash the password
  passwordHash = hashPassword(password)

  // Create user record
  newUser = {
    email: email,
    passwordHash: passwordHash,
    role: "pending", // Initial role, might need verification or family joining
    status: "pending_verification",
    createdAt: getCurrentTimestamp(),
    updatedAt: getCurrentTimestamp()
  }
  userId = Database.saveUser(newUser)

  // Send verification email
  verificationToken = generateVerificationToken(userId)
  sendVerificationEmail(email, verificationToken)

  RETURN success { userId: userId, message: "Registration successful, please verify your email." }
ENDFUNCTION
```

### 2. Email Verification

```pseudocode
// TDD Anchor: Test_VerifyEmail_WithValidToken_ActivatesUser
// TDD Anchor: Test_VerifyEmail_WithInvalidToken_ReturnsError
// TDD Anchor: Test_VerifyEmail_WithExpiredToken_ReturnsError

FUNCTION verifyEmail(token)
  // Validate token format (optional)

  // Find user by verification token
  tokenData = Database.findVerificationToken(token)
  IF tokenData IS NULL OR tokenData.isExpired() THEN
    RETURN error "Invalid or expired verification token"
  ENDIF

  // Find the user associated with the token
  user = Database.findUserById(tokenData.userId)
  IF user IS NULL THEN
    RETURN error "User not found for this token"
  ENDIF

  // Update user status
  user.status = "active"
  user.emailVerifiedAt = getCurrentTimestamp()
  user.updatedAt = getCurrentTimestamp()
  Database.updateUser(user)

  // Invalidate the token
  Database.deleteVerificationToken(token)

  RETURN success { message: "Email verified successfully." }
ENDFUNCTION
```

### 3. User Login (Email)

```pseudocode
// TDD Anchor: Test_Login_WithValidCredentials_ReturnsAuthToken
// TDD Anchor: Test_Login_WithInvalidEmail_ReturnsError
// TDD Anchor: Test_Login_WithIncorrectPassword_ReturnsError
// TDD Anchor: Test_Login_WithUnverifiedEmail_ReturnsError

FUNCTION loginUserWithEmail(email, password)
  // Input validation
  IF NOT isValidEmail(email) THEN
    RETURN error "Invalid email format"
  ENDIF

  // Find user by email
  user = Database.findUserByEmail(email)
  IF user IS NULL THEN
    RETURN error "User not found"
  ENDIF

  // Check user status
  IF user.status IS NOT "active" THEN
    IF user.status IS "pending_verification" THEN
      RETURN error "Please verify your email before logging in."
    ELSE
      RETURN error "Account is inactive or suspended."
    ENDIF
  ENDIF

  // Verify password
  IF NOT verifyPassword(password, user.passwordHash) THEN
    // Increment failed login attempts (optional)
    RETURN error "Incorrect password"
  ENDIF

  // Generate authentication token (e.g., JWT)
  authToken = generateAuthToken(user.id, user.role)

  // Update last login timestamp
  user.lastLogin = getCurrentTimestamp()
  Database.updateUser(user)

  RETURN success { authToken: authToken, user: { id: user.id, email: user.email, role: user.role } }
ENDFUNCTION
```

### 4. Password Reset Request

```pseudocode
// TDD Anchor: Test_RequestPasswordReset_WithValidEmail_SendsResetEmail
// TDD Anchor: Test_RequestPasswordReset_WithNonExistentEmail_ReturnsSuccessSilently

FUNCTION requestPasswordReset(email)
  // Input validation
  IF NOT isValidEmail(email) THEN
    RETURN error "Invalid email format"
  ENDIF

  // Find user by email
  user = Database.findUserByEmail(email)

  // IMPORTANT: Do not reveal if the email exists for security reasons
  IF user IS NOT NULL THEN
    // Generate password reset token
    resetToken = generatePasswordResetToken(user.id)

    // Send password reset email
    sendPasswordResetEmail(email, resetToken)
  ENDIF

  // Always return a success message to prevent email enumeration
  RETURN success { message: "If an account exists for this email, a password reset link has been sent." }
ENDFUNCTION
```

### 5. Password Reset Confirmation

```pseudocode
// TDD Anchor: Test_ResetPassword_WithValidTokenAndNewPassword_UpdatesPassword
// TDD Anchor: Test_ResetPassword_WithInvalidToken_ReturnsError
// TDD Anchor: Test_ResetPassword_WithExpiredToken_ReturnsError
// TDD Anchor: Test_ResetPassword_WithWeakNewPassword_ReturnsError

FUNCTION resetPassword(token, newPassword)
  // Validate token format (optional)

  // Find reset token data
  tokenData = Database.findPasswordResetToken(token)
  IF tokenData IS NULL OR tokenData.isExpired() THEN
    RETURN error "Invalid or expired password reset token"
  ENDIF

  // Find the user associated with the token
  user = Database.findUserById(tokenData.userId)
  IF user IS NULL THEN
    RETURN error "User not found for this token"
  ENDIF

  // Validate new password strength
  IF NOT isStrongPassword(newPassword) THEN
    RETURN error "New password does not meet complexity requirements"
  ENDIF

  // Hash the new password
  newPasswordHash = hashPassword(newPassword)

  // Update user's password
  user.passwordHash = newPasswordHash
  user.updatedAt = getCurrentTimestamp()
  Database.updateUser(user)

  // Invalidate the reset token
  Database.deletePasswordResetToken(token)

  RETURN success { message: "Password reset successfully." }
ENDFUNCTION
```

## Module: Chore Management (Initial)

### 1. Create Chore Template

```pseudocode
// TDD Anchor: Test_CreateChoreTemplate_WithValidData_SavesTemplate
// TDD Anchor: Test_CreateChoreTemplate_WithMissingTitle_ReturnsError
// TDD Anchor: Test_CreateChoreTemplate_ByChildRole_ReturnsPermissionError

FUNCTION createChoreTemplate(user, familyId, title, description, category, difficulty, estimatedDuration, pointValue)
  // Check user permissions (must be Parent or Admin)
  IF user.role IS NOT "parent" AND user.role IS NOT "admin" THEN
    RETURN error "Permission denied: Only parents or admins can create chores."
  ENDIF

  // Validate input data
  IF isEmpty(title) THEN
    RETURN error "Chore title cannot be empty."
  ENDIF
  // Add more validation for category, difficulty, duration, points...

  // Create chore template record
  newChore = {
    familyId: familyId,
    title: title,
    description: description,
    category: category,
    difficulty: difficulty,
    estimatedDuration: estimatedDuration,
    pointValue: pointValue, // Or calculate based on difficulty/duration
    createdBy: user.id,
    status: "active", // Template status
    createdAt: getCurrentTimestamp(),
    updatedAt: getCurrentTimestamp()
  }
  choreId = Database.saveChore(newChore)

  RETURN success { choreId: choreId, message: "Chore template created successfully." }
ENDFUNCTION
```

### 2. Assign Chore

```pseudocode
// TDD Anchor: Test_AssignChore_WithValidData_CreatesAssignment
// TDD Anchor: Test_AssignChore_ToNonFamilyMember_ReturnsError
// TDD Anchor: Test_AssignChore_WithInvalidChoreId_ReturnsError
// TDD Anchor: Test_AssignChore_WithPastDueDate_ReturnsError

FUNCTION assignChore(assignerUser, choreId, assigneeUserId, dueDate, recurringRule)
  // Check assigner permissions (must be Parent or Admin)
  IF assignerUser.role IS NOT "parent" AND assignerUser.role IS NOT "admin" THEN
    RETURN error "Permission denied: Only parents or admins can assign chores."
  ENDIF

  // Fetch chore template
  choreTemplate = Database.findChoreById(choreId)
  IF choreTemplate IS NULL THEN
    RETURN error "Chore template not found."
  ENDIF

  // Verify assignee is in the same family
  assigneeUser = Database.findUserById(assigneeUserId)
  IF assigneeUser IS NULL OR assigneeUser.familyId IS NOT assignerUser.familyId THEN
    RETURN error "Assignee not found or not in the same family."
  ENDIF

  // Validate schedule (dueDate or recurringRule)
  // Ensure dueDate is in the future, recurringRule is valid, etc.

  // Create assignment record
  newAssignment = {
    choreId: choreId,
    familyId: assignerUser.familyId,
    assignedTo: assigneeUserId,
    assignedBy: assignerUser.id,
    status: "pending",
    schedule: {
      type: IF recurringRule IS NOT NULL THEN "recurring" ELSE "one-time" ENDIF,
      dueDate: dueDate,
      recurring: recurringRule
    },
    createdAt: getCurrentTimestamp(),
    updatedAt: getCurrentTimestamp()
  }
  assignmentId = Database.saveAssignment(newAssignment)

  // Trigger notification to assignee
  sendNotification(assigneeUserId, "chore_assigned", { assignmentId: assignmentId, choreTitle: choreTemplate.title })

  RETURN success { assignmentId: assignmentId, message: "Chore assigned successfully." }
ENDFUNCTION
```

---

*Note: This pseudocode provides a starting point. Further modules (Rewards, Notifications, Dashboards, Mobile Sync) and more detailed logic within these functions will be developed iteratively.*
