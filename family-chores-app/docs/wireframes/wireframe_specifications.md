# Figma Wireframe Specifications

This document provides detailed specifications for creating wireframes in Figma for the Family Chores Application. These wireframes should serve as a visual guide for the UI/UX design and development teams.

## 1. Design System Components

Before creating individual screens, establish a design system with the following components:

### 1.1 Typography

- **Font Families**:
  - Primary: Inter (for general text)
  - Secondary: Montserrat (for headings)
  - Tertiary: Comic Sans MS (for child-focused elements)

- **Type Scale**:
  - Heading 1: 32px/40px, Bold
  - Heading 2: 24px/32px, Bold
  - Heading 3: 20px/28px, SemiBold
  - Heading 4: 18px/24px, SemiBold
  - Body Large: 16px/24px, Regular
  - Body: 14px/20px, Regular
  - Body Small: 12px/16px, Regular
  - Caption: 11px/16px, Regular

### 1.2 Color Palette

- **Primary Colors**:
  - Primary Blue: #4361EE (buttons, links, primary actions)
  - Secondary Green: #4CC9F0 (success, completion)
  - Accent Yellow: #F7B801 (highlights, notifications)
  - Accent Red: #E71D36 (errors, warnings)

- **Neutral Colors**:
  - Dark: #2B2D42 (text, icons)
  - Medium: #8D99AE (secondary text, borders)
  - Light: #EDF2F4 (backgrounds, cards)
  - White: #FFFFFF (page backgrounds)

- **Semantic Colors**:
  - Success: #4CC9F0
  - Warning: #F7B801
  - Error: #E71D36
  - Info: #4361EE

### 1.3 Component Library

Create reusable components for:

- **Buttons**:
  - Primary Button
  - Secondary Button
  - Tertiary Button
  - Icon Button
  - Toggle Button

- **Form Elements**:
  - Text Input
  - Dropdown
  - Checkbox
  - Radio Button
  - Toggle Switch
  - Date Picker
  - Time Picker

- **Cards**:
  - Chore Card
  - Reward Card
  - User Card
  - Notification Card
  - Achievement Card

- **Navigation**:
  - Top Navigation Bar
  - Bottom Navigation Bar (Mobile)
  - Sidebar Navigation (Desktop)
  - Breadcrumbs
  - Tabs

- **Feedback**:
  - Toast Notifications
  - Modal Dialogs
  - Progress Indicators
  - Loading States
  - Empty States

### 1.4 Iconography

Create a consistent icon set for:
- Chores (different categories)
- Rewards
- Users/Profiles
- Notifications
- Settings
- Navigation items
- Actions (add, edit, delete, etc.)

## 2. Web Application Wireframes

### 2.1 Authentication Screens

#### 2.1.1 Login Screen
- Logo at the top center
- Email/Username input field
- Password input field with show/hide toggle
- "Remember me" checkbox
- Login button (primary)
- "Forgot password?" link
- Social login options (Facebook, LinkedIn, GitHub)
- "Register" link for new users

#### 2.1.2 Registration Screen
- Logo at the top center
- Email input field
- Password input field with requirements indicator
- Confirm password field
- "Register with email" button (primary)
- Social registration options
- "Already have an account? Login" link
- Terms and privacy policy checkbox

#### 2.1.3 Forgot Password Screen
- Logo at the top center
- Email input field
- "Send reset link" button
- "Back to login" link

### 2.2 Onboarding Screens

#### 2.2.1 Role Selection Screen
- Welcome message
- Role options (Admin/Parent, Child)
- Description of each role
- "Continue" button

#### 2.2.2 Family Creation/Join Screen
- For Admin/Parent: Family name input, create family button
- For Child: Family code input, join family button
- Back button

#### 2.2.3 Profile Setup Screen
- Profile picture upload/selection
- First name, Last name inputs
- Display name input
- Age/Birth date input
- Bio/About me textarea
- "Complete profile" button

#### 2.2.4 Tutorial Screens (3-5 slides)
- Key features introduction
- Interactive elements highlighting
- Progress indicator
- "Skip tutorial" option
- "Next" and "Back" buttons

### 2.3 Dashboard Screens

#### 2.3.1 Child Dashboard
- Welcome message with user's name
- Today's chores section (3-4 cards)
- Points balance with visual indicator
- Upcoming chores section
- Recent achievements
- Available rewards teaser
- Bottom navigation (Dashboard, Chores, Rewards, Profile)

#### 2.3.2 Parent Dashboard
- Welcome message with user's name
- Family overview (members, total chores, completion rate)
- Action required section (approvals, assignments)
- Family activity feed
- Quick actions (add chore, add reward, invite member)
- Sidebar navigation (Dashboard, Chores, Rewards, Family, Reports, Settings)

### 2.4 Chore Management Screens

#### 2.4.1 Chore List Screen
- Filtering options (status, assignee, date range)
- Sorting options (due date, priority, points)
- List/Grid view toggle
- Chore cards with:
  - Title
  - Assignee
  - Due date
  - Status indicator
  - Priority indicator
  - Points value
- "Add new chore" button (for parents)
- Empty state design

#### 2.4.2 Chore Details Screen
- Chore title and description
- Difficulty and points
- Assignment details
- Due date/recurrence information
- Status with progress indicator
- Instructions/steps
- Evidence upload section (if applicable)
- Action buttons based on role and status
- Comments/feedback section

#### 2.4.3 Create/Edit Chore Screen
- Title input
- Description textarea
- Category dropdown
- Difficulty selection
- Points allocation (automatic or manual)
- Location input
- Instructions/steps builder
- Resources/links section
- Schedule section (one-time or recurring)
- Assignee selection
- Save/Cancel buttons

#### 2.4.4 Chore Approval Screen
- Chore details summary
- Evidence review section
- Approval/Rejection options
- Feedback textarea
- Points adjustment (if needed)
- Confirm button

### 2.5 Reward Management Screens

#### 2.5.1 Reward Catalog Screen
- Filtering options (category, points required)
- Sorting options (popularity, points)
- List/Grid view toggle
- Reward cards with:
  - Title
  - Image/icon
  - Points required
  - Category
  - Availability
- "Add new reward" button (for parents)
- Empty state design

#### 2.5.2 Reward Details Screen
- Reward title and description
- Points required
- Category
- Availability information
- Image/visual representation
- "Redeem" button with confirmation
- Related rewards section

#### 2.5.3 Create/Edit Reward Screen
- Title input
- Description textarea
- Category dropdown
- Points required input
- Image upload
- Availability settings (quantity, date range)
- Save/Cancel buttons

#### 2.5.4 Redemption Request Screen
- Reward details summary
- Points balance indicator
- Request note textarea
- Confirm/Cancel buttons

### 2.6 Family Management Screens

#### 2.6.1 Family Members Screen
- Member list with:
  - Profile picture
  - Name
  - Role
  - Status
  - Quick actions
- "Invite member" button
- Role management options

#### 2.6.2 Invite Member Screen
- Invitation code display
- Sharing options
- Manual email invitation
- Expiration settings
- Role pre-selection

#### 2.6.3 Family Settings Screen
- Family name and profile
- Chore settings section
- Reward settings section
- Notification preferences
- Privacy settings

### 2.7 Notification and Alerts Screens

#### 2.7.1 Notifications Center
- Filters (read/unread, type)
- Notification list with:
  - Icon by type
  - Title
  - Preview text
  - Timestamp
  - Read/unread indicator
- "Mark all as read" button
- Empty state design

#### 2.7.2 Notification Settings
- Channel preferences (in-app, email, push)
- Notification types toggles
- Quiet hours settings
- Frequency settings

### 2.8 Reporting and Analytics Screens

#### 2.8.1 Reports Dashboard
- Time period selector
- Report type selector
- Key metrics summary
- Visual charts and graphs
- Export options

#### 2.8.2 Chore Completion Report
- Completion rate by family member
- Completion rate by chore category
- Time-based trends
- Filtering options

#### 2.8.3 Points and Rewards Report
- Points earned by family member
- Points spent on rewards
- Most popular rewards
- Reward redemption patterns

## 3. Mobile Application Wireframes

### 3.1 Mobile-Specific Considerations

- Design for both iOS and Android patterns
- Bottom navigation with 4-5 key sections
- Swipe gestures for common actions
- Pull-to-refresh for content updates
- Floating action buttons for primary actions
- Optimized for one-handed operation
- Accommodate notches and home indicators

### 3.2 Key Mobile Screens

#### 3.2.1 Mobile Login/Registration
- Simplified forms
- Social login prominence
- Biometric authentication option

#### 3.2.2 Mobile Dashboard
- Focused on today's tasks
- Quick access to key functions
- Pull-down for refresh
- Notification badges

#### 3.2.3 Mobile Chore Details
- Swipeable between chores
- Camera access for evidence
- Voice input for comments

#### 3.2.4 Mobile Reward Redemption
- Quick redemption flow
- Points balance always visible
- Confirmation vibration

## 4. Responsive Design Breakpoints

Design wireframes for the following breakpoints:

- **Mobile**: 320px - 480px
- **Tablet**: 481px - 768px
- **Desktop Small**: 769px - 1024px
- **Desktop Large**: 1025px - 1440px
- **Extra Large**: 1441px+

## 5. Interactive Prototyping

Create interactive connections between screens to demonstrate:

- User registration and onboarding flow
- Chore assignment and completion flow
- Reward redemption flow
- Notification interaction flow
- Settings and configuration flow

## 6. Accessibility Considerations

- Ensure sufficient color contrast
- Design focus states for keyboard navigation
- Create touch targets of appropriate size (minimum 44x44px)
- Include text alternatives for visual elements
- Design for screen reader compatibility

## 7. Design Variations

### 7.1 Theme Variations
- Light theme (default)
- Dark theme
- High contrast theme

### 7.2 Age-Appropriate Variations
- Young children interface (simplified, more visual)
- Teen interface (more sophisticated, less childish)
- Parent interface (efficient, dashboard-focused)

## 8. Empty and Error States

Design appropriate empty and error states for:
- No chores assigned
- No rewards available
- No family members
- No notifications
- Search with no results
- Network connection errors
- Permission denied states

## 9. Loading States and Animations

Design:
- Skeleton screens for content loading
- Progress indicators for actions
- Transition animations between screens
- Micro-interactions for user feedback
- Celebration animations for achievements

## 10. Implementation Notes

- Create a shared Figma library for all components
- Use auto-layout for responsive components
- Organize frames and pages logically
- Include detailed annotations for developers
- Provide redline specifications for key components
- Create a design token system for easy theming