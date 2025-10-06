# StudyMate UI/UX Documentation

## Table of Contents
1. [Overview](#overview)
2. [Design System](#design-system)
3. [Page Documentation](#page-documentation)
4. [Component Library](#component-library)
5. [Responsive Design](#responsive-design)
6. [Accessibility](#accessibility)
7. [User Flows](#user-flows)

---

## Overview

### Purpose
This document provides comprehensive UI/UX specifications for StudyMate, a collaborative study application. It defines visual design standards, interaction patterns, and user experience guidelines to ensure consistency across all interfaces.

### Design Philosophy
- **Minimalist & Clean**: Focus on content with minimal visual noise
- **Modern & Professional**: Contemporary design with gradient accents
- **Accessible**: WCAG 2.1 AA compliance for inclusive design
- **Responsive**: Mobile-first approach with fluid layouts

---

## Design System

### Color Palette

#### Primary Colors
```css
--primary-blue: #1E3A8A     /* Main brand color - headers, CTAs */
--primary-light: #3B82F6     /* Lighter shade for gradients */
--secondary-green: #059669   /* Success states, active indicators */
--accent-orange: #EA580C     /* Warnings, important actions */
```

#### Neutral Colors
```css
--white: #FFFFFF
--gray-50: #F8FAFC          /* Backgrounds */
--gray-100: #F1F5F9         /* Message bubbles */
--gray-200: #E2E8F0         /* Borders, dividers */
--gray-400: #94A3B8         /* Placeholder text */
--gray-600: #64748B         /* Secondary text */
--gray-900: #1E293B         /* Primary text */
```

#### Semantic Colors
```css
--success: #10B981          /* Success messages, online status */
--error: #DC2626            /* Error states, danger actions */
--warning: #F59E0B          /* Warnings, admin badges */
--info: #0EA5E9             /* Information, notifications */
```

### Typography

#### Font Families
- **Primary**: 'Inter', sans-serif (body text, UI elements)
- **Monospace**: 'JetBrains Mono', monospace (timer display, codes)

#### Font Scales
```css
/* Headers */
h1: 1.375rem (22px) - 700 weight
h2: 1.25rem (20px) - 600 weight
h3: 1.125rem (18px) - 600 weight
h4: 1rem (16px) - 600 weight
h5: 0.95rem (15.2px) - 600 weight

/* Body */
Body text: 0.875rem (14px) - 400 weight
Small text: 0.8rem (12.8px) - 400 weight
Tiny text: 0.7rem (11.2px) - 400 weight

/* Special */
Timer display: clamp(2.5rem, 8vw, 3.5rem) - 700 weight
Button text: 0.875rem (14px) - 500 weight
```

### Spacing System
```css
/* Based on 0.25rem (4px) increments */
--space-1: 0.25rem   /* 4px */
--space-2: 0.5rem    /* 8px */
--space-3: 0.75rem   /* 12px */
--space-4: 1rem      /* 16px */
--space-5: 1.25rem   /* 20px */
--space-6: 1.5rem    /* 24px */
--space-8: 2rem      /* 32px */
--space-10: 2.5rem   /* 40px */
```

### Border Radius
```css
--radius-sm: 6px     /* Buttons, badges */
--radius-md: 8px     /* Inputs, cards */
--radius-lg: 12px    /* Containers, panels */
--radius-xl: 16px    /* Modals */
--radius-full: 50%   /* Avatars, circular buttons */
```

### Shadows
```css
--shadow-sm: 0 1px 3px rgba(0, 0, 0, 0.1)
--shadow-md: 0 4px 6px rgba(0, 0, 0, 0.1)
--shadow-lg: 0 8px 16px rgba(30, 58, 138, 0.3)
--shadow-xl: 0 25px 50px rgba(0, 0, 0, 0.25)
```

---

## Page Documentation

### 1. Login Page (`login.html`)

#### Layout
- **Container**: Centered card (400px max-width, 90% width on mobile)
- **Background**: Blue gradient (135deg, #1E3A8A to #3B82F6)
- **Card**: White background, 16px border-radius, large shadow
- **Vertical centering**: Flexbox centering on full viewport height

#### Components

**Logo**
- Image height: 88px
- Position: Centered at top of card

**Header**
- Title: "Welcome Back"
  - Font: h2, primary blue color
  - Weight: bold (700)
- Subtitle: "Login to continue using StudyMate"
  - Color: muted gray
  - Margin bottom: 1rem

**Form Fields**

1. Email Input
   - Label: "Email Address"
   - Placeholder: "your.email@example.com"
   - Type: email
   - Required field
   - Error message: "Please enter a valid email address."

2. Password Input
   - Label: "Password"
   - Placeholder: "Enter your password"
   - Type: password (toggleable)
   - Position: relative container
   - Toggle icon: Eye emoji (👁️) positioned absolute (right: 10px, top: 38px)
   - Error message: "Please enter your password."

3. Remember Me
   - Checkbox with label
   - Left-aligned

**Actions**
- Submit button: "Sign In"
  - Full width
  - Primary blue background
  - Hover: darker blue (#1E40AF)
- General error message area below button

**Footer Links**
- "Forgot your password?" link
- "New to StudyMate? Create an account" link
  - Links styled in primary blue with 600 weight

#### Interactions
- **Password Toggle**: Click eye icon to toggle password visibility
- **Validation**: 
  - Email format validation
  - Required field validation
  - Display inline error messages
- **Form Submit**: 
  - Prevent default
  - Validate all fields
  - Show loading state
  - Redirect to dashboard on success
  - Display error message on failure

---

### 2. Register Page (`register.html`)

#### Layout
Similar to login page structure with extended form

#### Components

**Logo & Header**
- Same as login page
- Title: "Create Account"
- Subtitle: "Join StudyMate and collaborate with peers"

**Form Fields**

1. Full Name
   - Label: "Full Name"
   - Placeholder: "Your full name"
   - Required
   - Error: "Please enter your full name."

2. Email Address
   - Same as login page
   - Error: "Please enter a valid email address."

3. Password
   - Label: "Password"
   - With toggle visibility
   - Minimum length validation
   - Strength indicators (optional)

4. Confirm Password
   - Label: "Confirm Password"
   - With toggle visibility
   - Must match password field
   - Real-time validation

5. Terms & Conditions
   - Checkbox required
   - Label with embedded link: "I agree to the Terms and Conditions"
   - Error: "You must agree to the Terms and Conditions."

**Notification Area**
- ID: `notification`
- Initially hidden
- Displays success/error messages
- Styles: padding 0.75rem, border-radius 8px, white text on colored background

**Actions**
- Submit button: "Register"
  - Full width, primary blue

**Footer**
- "Already have an account? Sign In" link

#### Interactions
- **Password Visibility**: Toggle for both password fields
- **Password Match**: Real-time validation that passwords match
- **Terms Validation**: Checkbox must be checked before submit
- **Email Format**: Validate email format
- **Form Submit**:
  - Validate all fields
  - Check password match
  - Verify terms accepted
  - Show notification on success/error
  - Redirect to login on successful registration

---

### 3. Dashboard Page (`dashboard.html`)

#### Layout Structure
```
┌─────────────────────────────────────────┐
│         Header (gradient blue)          │
├─────────────────────────────────────────┤
│         Stats Cards (3 columns)         │
├─────────────────────────────────────────┤
│         Quick Actions Card              │
├─────────────────────────────────────────┤
│         Search Bar                      │
├─────────────────────────────────────────┤
│   My Rooms Section / Search Results    │
├─────────────────────────────────────────┤
│         Public Rooms Section            │
└─────────────────────────────────────────┘
```

**Container**: Max-width 1400px, centered

#### Header Component

**Structure**
- Background: Linear gradient (135deg, #1E3A8A to #3B82F6)
- Padding: 1rem 1.5rem
- Box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1)

**Left Section (Brand)**
- Brand icon: 48x48px rounded square (12px radius)
  - Background: rgba(255, 255, 255, 0.2)
  - White icon color
  - Logo image alternative
- Brand title: "StudyMate"
  - Font-size: 1.375rem
  - Weight: 700
  - Color: white
- Brand subtitle: Welcome message with username
  - Font-size: 0.875rem
  - Status indicator: 8px green circle with pulse animation

**Right Section (Actions)**
- Profile button (optional)
  - Icon + text
  - Glassmorphic style
- Logout button
  - Red gradient background
  - Icon + "Logout" text

**Button Styles**
```css
background: rgba(255, 255, 255, 0.15);
backdrop-filter: blur(10px);
border: 1px solid rgba(255, 255, 255, 0.2);
padding: 0.5rem 1rem;
border-radius: 8px;
```

#### Stats Cards Section

**Grid**: 3 columns (responsive to 1 column on mobile)
**Gap**: 1rem

Each card:
- White background
- Padding: 1.5rem
- Border-radius: 12px
- Box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1)
- Text-align: center

**Card Content**:
1. **Study Sessions**
   - Value: Large number (1.8rem, bold, primary blue)
   - Label: "Study Sessions" (0.9rem, gray)
   
2. **Day Streak**
   - Same styling
   - Label: "Day Streak"

3. **Minutes Studied**
   - Same styling
   - Label: "Minutes Studied"

#### Quick Actions Card

**Styling**: Same as stats cards, full width
**Content**:
- Title: "Quick Actions" (h4, margin-bottom 0.75rem)
- Button: "Create New Study Room"
  - Full width
  - Primary blue gradient
  - Icon: Sparkle emoji
  - Padding: 0.6rem 1.2rem

#### Search Bar Card

**Styling**: Same card styling
**Content**:
- Title: "Find a Room" with search emoji
- Input field:
  - Placeholder: "Search by room name..."
  - Padding: 0.6rem 1rem
  - Border-radius: 8px
  - Border: 2px solid #e5e7eb
  - Focus: primary blue border with subtle box-shadow
  - Full width

#### Room Lists

**My Rooms Section**
- ID: `myRoomsSection`
- Initially hidden (display: none)
- Shows only when user has created/joined rooms
- Title: "My Study Rooms" with house emoji
- Section header: flex between title and potential actions

**Public Rooms Section**
- Title: "Public Study Rooms" with globe emoji
- Always visible unless search is active

**Search Results Section**
- ID: `searchResultsSection`
- Initially hidden
- Shows when user types in search
- Title: "Search Results" with magnifying glass emoji
- Replaces room lists during search

#### Room Card Component

**Structure**:
```
┌──────────────────────────────────────────┐
│ Room Name               [Public/Private] │
│ Status: Active/Ended                     │
│ Creator: Username                        │
│                           [Join Button]  │
└──────────────────────────────────────────┘
```

**Styling**:
```css
background: white;
border-radius: 12px;
padding: 1rem;
margin-bottom: 1rem;
display: flex;
justify-content: space-between;
box-shadow: 0 2px 6px rgba(0, 0, 0, 0.05);
transition: transform 0.2s, box-shadow 0.2s;
```

**Hover Effect**:
```css
transform: translateY(-2px);
box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
```

**Elements**:
1. Room Name (bold, larger font)
2. Privacy Badge:
   - Public: Blue background (#dbeafe), dark blue text (#1e40af)
   - Private: Yellow background (#fef3c7), brown text (#92400e)
   - Inline-block, padding 0.25rem 0.5rem, border-radius 6px
3. Status:
   - Active: Green color (#059669), bold
   - Ended: Gray color (#6b7280), bold
4. Creator name (smaller, gray)
5. Join button:
   - Primary blue background
   - White text
   - Padding: 0.5rem 1rem
   - Border-radius: 6px
   - Hover: darker blue

#### Empty States

**Structure**:
```css
text-align: center;
padding: 3rem 1rem;
color: #6b7280;
```

**Content**:
- Large icon (3rem font-size)
- Message text below
- Margin bottom: 0.5rem between elements

**Messages**:
- No rooms: Appropriate message for context
- No search results: "No rooms found matching your search"

#### Interactions

**Search Functionality**:
- Real-time filtering as user types
- Debounced to avoid excessive processing
- Shows/hides sections dynamically
- During search:
  - Hide "My Rooms" section
  - Hide "Public Rooms" section
  - Show "Search Results" section

**Create Room**:
- Click button → redirect to create-room.html

**Join Room**:
- Public room: Direct join, redirect to room page
- Private room: Prompt for password/code first

**Logout**:
- Clear session/token
- Redirect to login page

---

### 4. Create Room Page (`createRoom.html`)

#### Layout

**Navbar**:
- Background: Primary blue
- Brand: "StudyMate" (white, bold)
- Right: Logout button (outline-light)

**Main Container**:
- Centered card
- Max-width: 600px
- Margin: auto
- Padding: 1.5rem

#### Form Components

**Card Header**:
- Title: "Create Study Room" (h3)
- Margin-bottom: 1rem

**Form Fields**:

1. **Room Name**
   - Label: "Room Name"
   - Input: text
   - Placeholder: "Enter room name"
   - Required
   - Full width

2. **Study Interval**
   - Label: "Study Interval (minutes)"
   - Input: number
   - Placeholder: "e.g., 25"
   - Min: 5
   - Required
   - Help text (optional): "Recommended: 25 minutes"

3. **Break Interval**
   - Label: "Break Interval (minutes)"
   - Input: number
   - Placeholder: "e.g., 5"
   - Min: 1
   - Required
   - Help text (optional): "Recommended: 5 minutes"

4. **Privacy**
   - Label: "Privacy"
   - Select dropdown:
     - Option: "Public" (default)
     - Option: "Private (requires code)"
   - Required

5. **Room Code** (Conditional)
   - ID: `roomCodeDiv`
   - Initially hidden (display: none)
   - Shows when "Private" is selected
   - Label: "Room Code"
   - Input: text
   - Placeholder: "Enter room code"
   - Optional for user (generated if not provided)

**Submit Button**:
- Text: "Create Room"
- Full width
- Primary blue gradient
- Padding: 0.75rem 1.5rem
- Border-radius: 8px
- Font-weight: 600

#### Interactions

**Privacy Toggle**:
```javascript
// When privacy select changes
if (value === 'private') {
  show roomCodeDiv
} else {
  hide roomCodeDiv
}
```

**Form Validation**:
- Room name: Not empty
- Study interval: Minimum 5 minutes
- Break interval: Minimum 1 minute
- Intervals must be reasonable (max values suggested)

**Form Submit**:
1. Validate all fields
2. Create room object with settings
3. Send POST request to API
4. On success: Redirect to room page with room ID
5. On error: Show error message

---

### 5. Room Page (`room.html`)

#### Layout Structure

**Desktop (>1024px)**:
```
┌─────────────────────────────────────────┐
│              Header                     │
├──────┬──────────────────────┬───────────┤
│      │                      │           │
│ Par- │      Timer           │   Chat    │
│ tici-│      Section         │  Section  │
│ pants│                      │           │
│      │                      │           │
└──────┴──────────────────────┴───────────┘
```

**Widths**:
- Participants: 220px fixed
- Timer: flexible (flex: 1)
- Chat: 340px fixed

**Tablet/Mobile**: Single column, stacked vertically

#### Header Component

**Structure**:
```
┌─────────────────────────────────────────┐
│ [Icon] Room Name          [Btns] [Leave]│
│        Connected                         │
└─────────────────────────────────────────┘
```

**Styling**:
```css
background: linear-gradient(135deg, #1E3A8A, #3B82F6);
padding: 1rem 1.5rem;
display: flex;
justify-content: space-between;
box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
```

**Left Side (Room Info)**:

1. Room Icon
   - Size: 40x40px
   - Background: rgba(255, 255, 255, 0.2)
   - Border-radius: 10px
   - Icon: Book icon (bi-book)
   - Color: white

2. Room Details
   - Room Name:
     - Font-size: 1.125rem
     - Weight: 600
     - Color: white
     - Text-overflow: ellipsis
   - Connection Status:
     - Font-size: 0.75rem
     - Color: rgba(255, 255, 255, 0.8)
     - Status indicator: 8px green circle with pulse
     - Text: "Connected"

**Right Side (Actions)**:

Buttons (left to right):
1. Settings button
   - Icon: gear (bi-gear)
   - Text: "Settings"
2. Copy Link button
   - Icon: clipboard (bi-clipboard)
   - Text: "Copy Link"
3. Leave button
   - Icon: box-arrow-right
   - Text: "Leave"
   - Color: Red gradient
   - Style: danger variant

**Button Styling**:
```css
background: rgba(255, 255, 255, 0.15);
backdrop-filter: blur(10px);
border: 1px solid rgba(255, 255, 255, 0.2);
padding: 0.5rem 1rem;
border-radius: 8px;
gap: 0.375rem;
```

#### Loading Overlay

**When Active**:
```css
position: fixed;
top: 0; left: 0; right: 0; bottom: 0;
background: rgba(0, 0, 0, 0.7);
backdrop-filter: blur(5px);
z-index: 9999;
```

**Content**:
- Spinner: 50px circle, rotating animation
- Text: "Connecting to room..."
- Centered with flexbox

#### Participants Section (220px)

**Structure**:
```css
background: white;
border-radius: 12px;
padding: 1rem;
box-shadow: 0 1px 3px rgba(0, 0, 0, 0.1);
display: flex;
flex-direction: column;
```

**Section Header**:
- Title: "Participants" (font-weight: 600, primary blue)
- Count badge:
  - Background: #E0F2FE
  - Color: #1E3A8A
  - Border-radius: 12px
  - Padding: 0.125rem 0.5rem
  - Font-size: 0.75rem

**Participants List**:
- Scrollable (overflow-y: auto)
- Custom scrollbar styling

**Participant Card**:
```css
display: flex;
align-items: center;
gap: 0.625rem;
padding: 0.5rem;
border-radius: 8px;
transition: background 0.2s;
```

**Components**:
1. Avatar:
   - Size: 32x32px circle
   - Background: Dynamic color (based on username hash)
   - Color: white
   - Contains: First letter of name (uppercase)
   - Font-weight: 600
   - Status dot: 10px green circle (bottom-right)

2. Info:
   - Name: 0.875rem, weight 500, dark gray
   - Text-overflow: ellipsis
   - Admin badge (if applicable):
     - Gold star icon
     - Text: "Admin"
     - Color: #F59E0B
     - Font-size: 0.7rem

**Empty State**:
- Icon: people icon (2.5rem)
- Text: "No participants yet"
- Center aligned, gray color

#### Timer Section (Center)

**Container**:
```css
flex: 1;
display: flex;
flex-direction: column;
align-items: center;
justify-content: center;
background: white;
border-radius: 12px;
padding: 2rem 1rem;
```

**Session Tab**:
```css
background: linear-gradient(135deg, #E0F2FE, #DBEAFE);
color: #1E3A8A;
padding: 0.375rem 1rem;
border-radius: 20px;
font-size: 0.875rem;
font-weight: 600;
```
- Content: "1 / 4 Sessions" (dynamic)

**Timer Circle**:
```css
width: min(280px, 70vw);
height: min(280px, 70vw);
max-width: 320px;
max-height: 320px;
border-radius: 50%;
background: linear-gradient(135deg, #1E3A8A, #3B82F6);
display: flex;
flex-direction: column;
align-items: center;
justify-content: center;
box-shadow: 0 8px 16px rgba(30, 58, 138, 0.3);
position: relative;
```

**Circle Glow Effect**:
```css
::before {
  content: '';
  position: absolute;
  inset: -3px;
  border-radius: 50%;
  background: linear-gradient(135deg, #3B82F6, #1E3A8A);
  z-index: -1;
  opacity: 0.5;
  filter: blur(10px);
}
```

**Timer Display**:
- Font: JetBrains Mono
- Size: clamp(2.5rem, 8vw, 3.5rem)
- Weight: 700
- Color: white
- Text-shadow: 0 2px 8px rgba(0, 0, 0, 0.2)
- Content: "25:00" (dynamic)

**Phase Indicator**:
- Font-size: clamp(0.9rem, 3vw, 1.1rem)
- Weight: 500
- Color: rgba(255, 255, 255, 0.9)
- Content: "Study Time" or "Break Time"

**Timer Controls**:
```css
display: flex;
gap: 1rem;
margin-top: 1.5rem;
```

**Control Buttons**:

1. Skip Button (⏭):
   - Size: 48x48px circle
   - Background: #E2E8F0
   - Color: #64748B

2. Play/Pause Button (▶):
   - Size: 64x64px circle
   - Background: linear-gradient(135deg, #059669, #10B981)
   - Color: white
   - Larger than others
   - Icon changes: ▶ (play) / ⏸ (pause)

3. Reset Button (⏹):
   - Size: 48x48px circle
   - Background: #E2E8F0
   - Color: #64748B

**Button Interactions**:
```css
hover: transform: translateY(-2px);
       box-shadow: 0 4px 8px rgba(0, 0, 0, 0.15);
active: transform: translateY(0);
disabled: opacity: 0.5; cursor: not-allowed;
```

#### Chat Section (340px)

**Container**:
```css
width: 340px;
display: flex;
flex-direction: column;
background: white;
border-radius: 12px;
padding: 1rem;
min-height: 0;
```

**Chat Header**:
- Title: "Chat"
- Same styling as participants header
- Border-bottom: 2px solid #E2E8F0

**Messages Area**:
```css
flex: 1;
overflow-y: auto;
padding: 0.5rem 0;
min-height: 0;
position: relative;
```

**Message Component**:

**Structure for Other Users**:
```
┌────────────────────────────────┐
│ [Avatar] Name • Time           │
│          Message text in bubble│
└────────────────────────────────┘
```

**Structure for Own Messages**:
```
┌────────────────────────────────┐
│           Time • Name [Avatar] │
│ Message text in bubble         │
└────────────────────────────────┘
```

**Message Styling**:
```css
display: flex;
gap: 0.5rem;
margin-bottom: 0.75rem;
animation: fadeIn 0.3s;
```

**Own Messages**:
```css
flex-direction: row-reverse;
```

**Avatar** (32x32px):
- Same as participant avatar
- Dynamic background color

**Message Content**:

1. Header:
   - Sender name (0.7rem, weight 600, primary blue)
   - Timestamp (0.65rem, gray)
   - Separated by bullet •
   - Own messages: reversed order

2. Bubble:
   - Other users:
     ```css
     background: #F1F5F9;
     border-bottom-left-radius: 4px;
     ```
   - Own messages:
     ```css
     background: linear-gradient(135deg, #059669, #10B981);
     color: white;
     border-bottom-right-radius: 4px;
     ```
   - Common:
     ```css
     padding: 0.625rem 0.875rem;
     border-radius: 12px;
     font-size: 0.875rem;
     line-height: 1.5;
     word-break: break-word;
     ```

**System Messages**:
```css
text-align: center;
font-size: 0.75rem;
color: #94A3B8;
padding: 0.5rem;
background: #F8FAFC;
border-radius: 8px;
margin: 0.75rem 0;
```

**Typing Indicator**:
```css
display: none;
padding: 0.5rem;
color: #64748B;
font-size: 0.8rem;
font-style: italic;
```
- Shows when another user is typing
- Text: "Someone is typing..."

**Scroll to Bottom Button**:
```css
position: absolute;
bottom: 0.5rem;
right: 0.5rem;
background: #3B82F6;
color: white;
width: 32px;
height: 32px;
border-radius: 50%;
display: none; /* shows when scrolled up */
box-shadow: 0 2px 8px rgba(0, 0, 0, 0.2);
```

**Chat Input Area**:
```css
display: flex;
gap: 0.5rem;
padding-top: 0.75rem;
border-top: 1px solid #E2E8F0;
```

**Textarea**:
```css
flex: 1;
padding: 0.625rem 0.875rem;
border: 1px solid #E2E8F0;
border-radius: 8px;
resize: none;
font-size: 0.875rem;
font-family: 'Inter', sans-serif;
rows: 1; /* auto-expands */
```

**Send Button**:
```css
background: linear-gradient(135deg, #1E3A8A, #3B82F6);
color: white;
padding: 0 1.25rem;
border-radius: 8px;
font-size: 0.875rem;
font-weight: 500;
```

#### Settings Modal

**Modal Structure**:
```css
.modal-content {
  border-radius: 16px;
  box-shadow: 0 20px 25px -5px rgba(0, 0, 0, 0.1);
}
```

**Modal Header**:
```css
background: linear-gradient(135deg, #1E3A8A, #3B82F6);
color: white;
border-radius: 16px 16px 0 0;
padding: 1.25rem 1.5rem;
```
- Title: "Room Settings"
- Close button (white)

**Modal Body Sections**:

**1. Room Information** (Read-only):

Display grid with info items:
```css
.info-item {
  display: flex;
  justify-content: space-between;
  padding: 0.75rem;
  background: #F8FAFC;
  border-radius: 8px;
  gap: 1rem;
}
```

Items:
- Room Name
- Created by
- Created on (date)
- Privacy (Public/Private)
- Room Code (only for private, with copy button)
- Current Admin
- Total Sessions

**2. Room Controls** (Admin Only):

Admin Note:
```css
background: #FEF3C7;
border-left: 3px solid #F59E0B;
padding: 0.75rem;
font-size: 0.8rem;
color: #64748B;
font-style: italic;
```
- Text: "Only the room admin can modify these settings."
- Icon: shield-check

**Control Groups**:

1. **Edit Room Name**:
   - Label: "Room Name" with tag icon
   - Input field + Save button
   - Button disabled until input changes
   - Primary blue save button

2. **Edit Timer Intervals**:
   - Label: "Timer Intervals" with clock icon
   - Two number inputs (row, 2 columns):
     - Study (minutes): min 1, max 120
     - Break (minutes): min 1, max 30
   - Save Intervals button (full width, small)
   - Initially disabled for non-admins

3. **Change Password** (Private rooms only):
   - ID: `changePasswordGroup`
   - Label: "Change Room Password" with key icon
   - Input + Change button
   - Only visible for private rooms

4. **Manage Participants**:
   - Label: "Manage Participants" with people icon
   - Scrollable list (max-height: 220px)
   - Custom scrollbar
   
   **Participant Item**:
   ```css
   display: flex;
   justify-content: space-between;
   align-items: center;
   padding: 0.625rem;
   background: white;
   border: 1px solid #E2E8F0;
   border-radius: 8px;
   margin-bottom: 0.5rem;
   ```
   
   Components:
   - Avatar (32px) + Name
   - Kick button:
     ```css
     background: #DC2626;
     color: white;
     padding: 0.375rem 0.875rem;
     border-radius: 6px;
     font-size: 0.75rem;
     ```

5. **Danger Zone**:
   ```css
   border: 2px solid #FEE2E2;
   padding: 1.25rem;
   border-radius: 12px;
   background: #FEF2F2;
   ```
   
   - Label: "Danger Zone" (red text, exclamation icon)
   - End Room button:
     - Full width
     - Red background
     - Text: "End Room"
     - Initially disabled for non-admins
   - Help text: "This will end the session and kick all participants."

#### Interactions & Behavior

**Timer Sync**:
- All participants see the same timer state
- Only admin can control timer (start/pause/skip/reset)
- Timer updates broadcast via WebSocket
- Visual/audio alerts on phase transitions

**Chat**:
- Real-time messaging via Socket.io
- Enter key sends message
- Shift+Enter for new line
- Auto-scroll on new messages
- Scroll-to-bottom button appears when scrolled up
- Typing indicators show when others type
- Messages persist for session duration

**Settings Modal**:
- Opens on Settings button click
- Admin controls enabled only for room creator
- Non-admins see read-only view
- Changes apply immediately on save
- Confirmation for destructive actions (kick, end room)

**Leave Room**:
- Confirmation dialog
- Disconnects user from room
- Removes from participant list
- Redirects to dashboard

**Copy Link/Code**:
- Copies room URL to clipboard
- Shows toast notification: "Link copied!"
- For private rooms, includes code in share format

---

## Component Library

### Buttons

#### Primary Button
```css
background: linear-gradient(135deg, #1E3A8A, #3B82F6);
color: white;
padding: 0.5rem 1rem;
border-radius: 8px;
font-size: 0.875rem;
font-weight: 500;
border: none;
cursor: pointer;
transition: all 0.2s;
```

**Hover**:
```css
transform: translateY(-1px);
box-shadow: 0 4px 8px rgba(30, 58, 138, 0.3);
```

**Active**:
```css
transform: translateY(0);
```

**Disabled**:
```css
opacity: 0.5;
cursor: not-allowed;
```

#### Secondary Button (Header)
```css
background: rgba(255, 255, 255, 0.15);
backdrop-filter: blur(10px);
border: 1px solid rgba(255, 255, 255, 0.2);
color: white;
padding: 0.5rem 1rem;
border-radius: 8px;
font-size: 0.875rem;
font-weight: 500;
```

**Hover**:
```css
background: rgba(255, 255, 255, 0.25);
transform: translateY(-1px);
```

#### Danger Button
```css
background: rgba(220, 38, 38, 0.9);
border: 1px solid rgba(220, 38, 38, 1);
color: white;
/* Other properties same as secondary */
```

**Hover**:
```css
background: rgba(185, 28, 28, 1);
```

#### Circular Control Button
```css
width: 48px;
height: 48px;
border-radius: 50%;
border: none;
cursor: pointer;
display: flex;
align-items: center;
justify-content: center;
font-size: 1.2rem;
background: #E2E8F0;
color: #64748B;
transition: all 0.2s;
box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
```

**Play Button Variant**:
```css
width: 64px;
height: 64px;
background: linear-gradient(135deg, #059669, #10B981);
color: white;
font-size: 1.5rem;
```

### Input Fields

#### Text Input
```css
padding: 0.625rem 0.875rem;
border: 1px solid #E2E8F0;
border-radius: 8px;
font-size: 0.875rem;
font-family: 'Inter', sans-serif;
transition: border-color 0.2s;
width: 100%;
```

**Focus**:
```css
outline: none;
border-color: #3B82F6;
```

**Error State**:
```css
border-color: #DC2626;
```

#### Number Input
Same as text input with additional:
```css
/* Remove spinner buttons for cleaner look (optional) */
-moz-appearance: textfield;
```

```css
::-webkit-outer-spin-button,
::-webkit-inner-spin-button {
  -webkit-appearance: none;
  margin: 0;
}
```

#### Textarea
```css
resize: none;
font-family: 'Inter', sans-serif;
min-height: 40px;
max-height: 120px;
/* Other properties same as text input */
```

Auto-resize behavior via JavaScript

#### Select Dropdown
```css
padding: 0.625rem 0.875rem;
border: 1px solid #E2E8F0;
border-radius: 8px;
font-size: 0.875rem;
background: white;
cursor: pointer;
/* Same focus state as text input */
```

### Cards

#### Standard Card
```css
background: white;
border-radius: 12px;
padding: 1rem;
box-shadow: 0 1px 3px rgba(0, 0, 0, 0.1);
border: 1px solid #E2E8F0;
```

#### Stat Card
```css
/* Extends standard card */
text-align: center;
padding: 1.5rem;
```

**Content**:
- Value: 1.8rem, bold, primary blue
- Label: 0.9rem, gray-600

#### Room Card
```css
/* Extends standard card */
display: flex;
justify-content: space-between;
align-items: center;
margin-bottom: 1rem;
transition: transform 0.2s, box-shadow 0.2s;
```

**Hover**:
```css
transform: translateY(-2px);
box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
```

#### Auth Card (Login/Register)
```css
border-radius: 16px;
padding: 2.5rem;
background: white;
max-width: 400px;
box-shadow: 0 25px 50px rgba(0, 0, 0, 0.25);
```

### Badges

#### Count Badge
```css
background: #E0F2FE;
color: #1E3A8A;
padding: 0.125rem 0.5rem;
border-radius: 12px;
font-size: 0.75rem;
font-weight: 600;
display: inline-block;
```

#### Privacy Badge - Public
```css
background: #DBEAFE;
color: #1E40AF;
padding: 0.25rem 0.5rem;
border-radius: 6px;
font-size: 0.75rem;
font-weight: 600;
display: inline-block;
```

#### Privacy Badge - Private
```css
background: #FEF3C7;
color: #92400E;
/* Other properties same as public */
```

#### Status Badge - Active
```css
color: #059669;
font-weight: bold;
```

#### Status Badge - Ended
```css
color: #6b7280;
font-weight: bold;
```

#### Admin Badge
```css
display: inline-flex;
align-items: center;
gap: 0.25rem;
font-size: 0.7rem;
color: #F59E0B;
```

Icon: Gold star

#### Session Counter Badge
```css
background: linear-gradient(135deg, #E0F2FE, #DBEAFE);
color: #1E3A8A;
font-weight: 600;
padding: 0.375rem 1rem;
border-radius: 20px;
font-size: 0.875rem;
box-shadow: 0 2px 4px rgba(0, 0, 0, 0.05);
```

### Avatars

#### Participant Avatar
```css
width: 32px;
height: 32px;
border-radius: 50%;
background: #3B82F6; /* Dynamic per user */
color: white;
display: flex;
align-items: center;
justify-content: center;
font-weight: 600;
font-size: 0.8rem;
position: relative;
flex-shrink: 0;
```

**Content**: First letter of username (uppercase)

**Color Generation**: Hash username to generate consistent color

#### Room Icon
```css
width: 40px;
height: 40px;
background: rgba(255, 255, 255, 0.2);
border-radius: 10px;
display: flex;
align-items: center;
justify-content: center;
color: white;
font-size: 1.25rem;
flex-shrink: 0;
```

#### Brand Icon (Dashboard)
```css
width: 48px;
height: 48px;
background: rgba(255, 255, 255, 0.2);
border-radius: 12px;
display: flex;
align-items: center;
justify-content: center;
color: white;
font-size: 1.5rem;
flex-shrink: 0;
```

#### Status Dot
```css
position: absolute;
bottom: 0;
right: 0;
width: 10px;
height: 10px;
background: #10B981;
border: 2px solid white;
border-radius: 50%;
```

#### Status Indicator (Header)
```css
width: 8px;
height: 8px;
background: #10B981;
border-radius: 50%;
animation: pulse 2s infinite;
```

### Messages

#### Message Container
```css
display: flex;
gap: 0.5rem;
margin-bottom: 0.75rem;
animation: fadeIn 0.3s;
```

**Own Message Variant**:
```css
flex-direction: row-reverse;
```

#### Message Avatar
Same as participant avatar (32px)

#### Message Content
```css
flex: 1;
min-width: 0;
max-width: 75%;
```

**Own Message Alignment**:
```css
display: flex;
flex-direction: column;
align-items: flex-end;
```

#### Message Header
```css
display: flex;
gap: 0.5rem;
align-items: center;
font-size: 0.7rem;
margin-bottom: 0.25rem;
color: #64748B;
```

**Own Message Variant**:
```css
flex-direction: row-reverse;
```

**Elements**:
- Sender name: 600 weight, primary blue
- Timestamp: 0.65rem, gray-400

#### Message Bubble - Others
```css
background: #F1F5F9;
padding: 0.625rem 0.875rem;
border-radius: 12px;
border-bottom-left-radius: 4px;
font-size: 0.875rem;
line-height: 1.5;
word-break: break-word;
```

#### Message Bubble - Own
```css
background: linear-gradient(135deg, #059669, #10B981);
color: white;
border-bottom-right-radius: 4px;
/* Other properties same as others */
```

#### System Message
```css
text-align: center;
font-size: 0.75rem;
color: #94A3B8;
margin: 0.75rem 0;
padding: 0.5rem;
background: #F8FAFC;
border-radius: 8px;
animation: fadeIn 0.3s;
```

#### Blocked Message
```css
/* Extends system message */
color: #b91c1c;
background-color: #fee2e2;
```

### Modals

#### Modal Container
```css
.modal-content {
  border-radius: 16px;
  border: none;
  box-shadow: 0 20px 25px -5px rgba(0, 0, 0, 0.1);
}
```

#### Modal Header
```css
background: linear-gradient(135deg, #1E3A8A, #3B82F6);
color: white;
border-radius: 16px 16px 0 0;
padding: 1.25rem 1.5rem;
border: none;
```

**Title**:
```css
font-weight: 600;
font-size: 1.125rem;
```

**Close Button**:
```css
filter: brightness(0) invert(1);
opacity: 0.8;
```

#### Modal Body
```css
padding: 1.5rem;
```

### Lists & Scrollable Areas

#### Scrollbar Styling
```css
/* Webkit browsers */
::-webkit-scrollbar {
  width: 6px;
}

::-webkit-scrollbar-track {
  background: #F1F5F9;
  border-radius: 10px;
}

::-webkit-scrollbar-thumb {
  background: #CBD5E1;
  border-radius: 10px;
}

::-webkit-scrollbar-thumb:hover {
  background: #94A3B8;
}
```

Applied to:
- `.chat-messages`
- `.participants-list`
- `.participants-manage`

### Loading States

#### Loading Overlay
```css
position: fixed;
top: 0;
left: 0;
right: 0;
bottom: 0;
background: rgba(0, 0, 0, 0.7);
display: flex;
align-items: center;
justify-content: center;
z-index: 9999;
backdrop-filter: blur(5px);
```

#### Spinner
```css
width: 50px;
height: 50px;
border: 4px solid rgba(255, 255, 255, 0.3);
border-top-color: white;
border-radius: 50%;
animation: spin 1s linear infinite;
```

### Empty States

```css
text-align: center;
padding: 3rem 1rem;
color: #6b7280;
```

**Icon**:
```css
font-size: 3rem;
margin-bottom: 1rem;
opacity: 0.5;
```

**Text**:
```css
font-size: 0.875rem;
margin: 0;
```

---

## Responsive Design

### Breakpoints

```css
/* Mobile Small */
@media (max-width: 480px) { }

/* Mobile */
@media (max-width: 768px) { }

/* Tablet */
@media (max-width: 1024px) { }

/* Desktop */
@media (min-width: 1025px) { }
```

### Responsive Behavior by Page

#### Dashboard Page

**Desktop (>768px)**:
- Stats cards: 3-column grid
- Full header with text labels
- Normal padding and spacing

**Mobile (<768px)**:
- Stats cards: 1-column stack
- Header buttons: Icon only, hide text
- Reduced padding (1rem → 0.875rem)
- Brand icon: 48px → 40px
- Font sizes: Slightly reduced

#### Room Page

**Desktop (>1024px)**:
- Three-column layout: Participants (220px) | Timer (flex) | Chat (340px)
- Horizontal arrangement
- Full button labels

**Tablet (768px - 1024px)**:
- Single column, vertical stack
- Order: Timer → Participants → Chat
- All sections: 100% width
- Max-height constraints: 280px for side sections
- Overflow: scroll

**Mobile (<768px)**:
- Same layout as tablet
- Further reduced sizes:
  - Timer circle: 220px → 200px
  - Control buttons: 48px → 40px (44px → 54px for play)
  - Header padding: 1rem → 0.875rem → 0.75rem
  - Room icon: 40px → 36px
  - Font sizes reduced
- Button text: Hidden, icon only
- Sections max-height: 240px

**Mobile Small (<480px)**:
- Minimal padding: 0.75rem
- Timer circle: 200px minimum
- Session tab: 0.8rem font
- Control buttons: 40px (54px for play)
- Very compact spacing

#### Auth Pages (Login/Register)

**Desktop**:
- Card: 400px max-width
- Full padding: 2.5rem
- Logo: 88px height

**Mobile**:
- Card: 90% width
- Maintain padding
- Responsive font sizes
- Touch-friendly input heights

#### Create Room Page

**All Sizes**:
- Card: Max-width 600px
- Responsive to container
- Form fields: 100% width
- Stacks naturally on mobile

### Responsive Typography

Uses `clamp()` for fluid scaling:

```css
/* Timer display */
font-size: clamp(2.5rem, 8vw, 3.5rem);

/* Phase indicator */
font-size: clamp(0.9rem, 3vw, 1.1rem);

/* Timer circle size */
width: min(280px, 70vw);
height: min(280px, 70vw);
```

### Touch Targets

Minimum touch target: **44x44px** (iOS/Android guidelines)

Applies to:
- All buttons
- Input fields (min-height: 44px)
- Clickable list items
- Toggle switches
- Close buttons

### Mobile Optimizations

**Performance**:
- Hardware acceleration: `transform: translateZ(0)`
- Minimize repaints
- Optimize animations
- Lazy load images

**UX**:
- Larger tap areas
- No hover states (`:hover` → `:active`)
- Prevent zoom on input focus: `font-size >= 16px`
- Fixed positioning for headers
- Bottom sheets instead of modals (optional)

**Gestures**:
- Swipe to dismiss (optional)
- Pull to refresh (optional)
- Tap to scroll to top

---

## Accessibility

### WCAG 2.1 AA Compliance

#### Color Contrast Ratios

**Text Contrast** (4.5:1 minimum):
- Primary text (#1E293B) on white: 13.2:1 ✓
- Secondary text (#64748B) on white: 5.9:1 ✓
- Link text (#1E3A8A) on white: 9.4:1 ✓

**Large Text** (3:1 minimum):
- Headers, buttons: All pass

**UI Components** (3:1 minimum):
- Borders, focus indicators: All pass
- Button backgrounds: Sufficient contrast

**Issue Areas**:
- White text on gradient buttons: Check contrast
- Light gray placeholder text: May need darkening for some users

#### Keyboard Navigation

**Tab Order**:
- Logical flow: top to bottom, left to right
- Skip to main content link (optional)
- All interactive elements tabbable

**Focus Indicators**:
```css
:focus {
  outline: 2px solid #3B82F6;
  outline-offset: 2px;
}

/* Or custom */
:focus-visible {
  box-shadow: 0 0 0 3px rgba(59, 130, 246, 0.5);
}
```

**Keyboard Shortcuts**:
- Enter: Submit forms, activate buttons
- Space: Activate buttons, toggle checkboxes
- Escape: Close modals, cancel actions
- Arrow keys: Navigate lists (optional)
- Tab: Move forward
- Shift+Tab: Move backward

#### Screen Reader Support

**Semantic HTML**:
```html
<header>, <nav>, <main>, <section>, <article>, <aside>, <footer>
```

**ARIA Labels**:
```html
<!-- Icon-only buttons -->
<button aria-label="Settings">
  <i class="bi bi-gear"></i>
</button>

<!-- Status indicators -->
<div role="status" aria-live="polite">
  Connected
</div>

<!-- Loading states -->
<div role="alert" aria-busy="true">
  Loading...
</div>
```

**Form Labels**:
```html
<label for="email">Email Address</label>
<input id="email" type="email" required>
```

**Error Messages**:
```html
<input aria-describedby="email-error" aria-invalid="true">
<div id="email-error" role="alert">
  Please enter a valid email
</div>
```

**Hidden Content**:
```html
<!-- Decorative icons -->
<i class="bi-star" aria-hidden="true"></i>

<!-- Screen reader only text -->
<span class="sr-only">Loading...</span>
```

#### Form Accessibility

**Labels**:
- Every input has associated label
- `for` attribute matches input `id`
- Labels visible at all times (no placeholder-only)

**Required Fields**:
```html
<input required aria-required="true">
```

**Error Handling**:
- Inline error messages
- `aria-invalid="true"` on error
- `aria-describedby` links to error message
- Error summary at top of form (optional)

**Autocomplete**:
```html
<input autocomplete="email">
<input autocomplete="current-password">
<input autocomplete="new-password">
```

#### Interactive Feedback

**Button States**:
```css
/* Normal */
button { }

/* Hover */
button:hover { }

/* Focus */
button:focus-visible { }

/* Active */
button:active { }

/* Disabled */
button:disabled {
  opacity: 0.5;
  cursor: not-allowed;
}
```

**Loading States**:
- Disable buttons during loading
- Show spinner or loading text
- `aria-busy="true"`
- Prevent duplicate submissions

**Success/Error Feedback**:
- Visual indicators (color, icons)
- Text descriptions (not color-only)
- Toast notifications
- `role="alert"` for important messages

#### Motion & Animation

**Reduced Motion**:
```css
@media (prefers-reduced-motion: reduce) {
  * {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
  }
}
```

**Safe Animations**:
- Fade in/out: Safe
- Slide: Safe
- Pulse: Safe (not too fast)
- Spin: Use for loading only
- Flash: Avoid (seizure risk)

#### Color & Contrast

**Not Color-Only**:
- Use icons + color for status
- Use text labels with colored badges
- Pattern fills in addition to color (charts)

**Dark/Light Modes**:
- Maintain contrast ratios in both modes
- Test with different system preferences

**Color Blindness**:
- Success: Green + checkmark
- Error: Red + X icon
- Warning: Orange + exclamation
- Info: Blue + info icon

---

## User Flows

### 1. New User Registration

```
1. User lands on login page
2. Clicks "Create an account" link
   ↓
3. Register page loads
4. User fills form:
   - Full name
   - Email
   - Password
   - Confirm password
   - Accept terms
   ↓
5. Real-time validation:
   - Email format
   - Password strength
   - Passwords match
   - Terms accepted
   ↓
6. Submit form
   ↓
7. Server validation:
   - Email not already registered
   - Password meets requirements
   ↓
8. Success:
   - Show success notification
   - Redirect to login (after 2s)
   ↓
9. Error:
   - Show error notification
   - Keep user on page
   - Highlight problem fields
```

### 2. User Login

```
1. User on login page
2. Enter credentials:
   - Email
   - Password
   - (Optional) Remember me
   ↓
3. Real-time validation:
   - Email format
   - Password not empty
   ↓
4. Submit form
   ↓
5. Server authentication:
   - Verify credentials
   - Generate JWT token
   ↓
6. Success:
   - Store token (localStorage/cookie)
   - Redirect to dashboard
   ↓
7. Error:
   - Show error message
   - Clear password field
   - Keep email filled
   - Focus on password
```

### 3. Create Study Room

```
1. User on dashboard
2. Click "Create New Study Room"
   ↓
3. Create room page loads
4. Fill form:
   - Room name (required)
   - Study interval (default: 25 min)
   - Break interval (default: 5 min)
   - Privacy (default: Public)
   ↓
5. If Private selected:
   - Room code field appears
   - (Optional) Enter custom code
   ↓
6. Validation:
   - Room name not empty
   - Intervals within limits (1-120 min study, 1-30 min break)
   ↓
7. Submit form
   ↓
8. Server creates room:
   - Generate room ID
   - Generate code (if private and not provided)
   - Set creator as admin
   ↓
9. Success:
   - Redirect to room page
   - User joins automatically
   ↓
10. Error:
   - Show error message
   - Keep form filled
```

### 4. Join Public Room

```
1. User on dashboard
2. Browse public rooms list
   OR
   Search for specific room
   ↓
3. Find desired room
4. Click "Join" button
   ↓
5. Loading state:
   - Show spinner
   - Disable button
   ↓
6. Server validation:
   - Room exists
   - Room not full (if limit exists)
   - Room still active
   ↓
7. Success:
   - Redirect to room page
   - Connect via WebSocket
   - Add to participants list
   ↓
8. Error:
   - Show error toast
   - Keep user on dashboard
```

### 5. Join Private Room

```
1. User has room link/code
2. Options:
   A. Click shared link → auto-redirect
   B. Enter code manually on dashboard
   ↓
3. Prompt for room code (if not in URL)
   ↓
4. Submit code
   ↓
5. Server validation:
   - Code matches room
   - Room exists and active
   ↓
6. Success:
   - Redirect to room
   - Join as participant
   ↓
7. Error:
   - "Invalid code" message
   - Allow retry
```

### 6. Study Session Flow

```
1. User joins room
2. Loading overlay:
   - "Connecting to room..."
   - Connect WebSocket
   - Fetch room state
   ↓
3. Room loads:
   - Show participants
   - Show current timer state
   - Load chat history
   ↓
4. Participants see:
   - Timer (synced)
   - Other participants
   - Chat messages
   ↓
5. Admin starts session:
   - Click Play button
   - Timer starts for all
   - Broadcast start event
   ↓
6. Study phase:
   - Timer counts down
   - Users can chat
   - "Study Time" indicator
   ↓
7. Phase ends:
   - Audio/visual alert
   - Switch to break phase
   - "Break Time" indicator
   ↓
8. Break phase:
   - Shorter timer
   - Users can chat, rest
   ↓
9. Cycle repeats:
   - Back to study phase
   - Session counter increments
   - Continue until target sessions
   ↓
10. Session complete:
    - Log progress to database
    - Show completion message
    - Update user stats
    - Option to start new session
```

### 7. Chat Interaction

```
1. User in room
2. Type message in textarea
   ↓
3. Optional: Other users see typing indicator
   ↓
4. Press Enter or click Send
   ↓
5. Message validation:
   - Not empty
   - Length within limits
   ↓
6. Send via WebSocket:
   - Broadcast to all participants
   - Include timestamp, sender info
   ↓
7. Receive message:
   - All users see message appear
   - Animate in (fadeIn)
   - Auto-scroll to bottom
   ↓
8. Message display:
   - Others: Left-aligned, gray bubble
   - Own: Right-aligned, green bubble
   - System: Centered, light gray
   ↓
9. Continuous chat:
   - History persists for session
   - Scroll freely
   - Scroll-to-bottom button if scrolled up
```

### 8. Admin Room Management

```
1. Admin opens Settings modal
2. View room information (read-only)
   ↓
3. Available admin actions:
   A. Edit room name
   B. Change timer intervals
   C. Change password (private rooms)
   D. Manage participants (kick users)
   E. End room
   ↓
4A. Edit Room Name:
    - Type new name
    - Click Save
    - Update room name everywhere
    - Broadcast to all participants
    ↓
4B. Change Intervals:
    - Adjust study/break times
    - Click Save Intervals
    - Apply on next session start
    - (Current session not affected)
    ↓
4C. Change Password:
    - Enter new password
    - Click Change
    - Update room code
    -
