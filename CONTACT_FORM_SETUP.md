# Contact Form Setup Guide

## Overview
The contact form has been successfully added to your landing page with the following features:
- Responsive contact form on the landing page
- Email integration with nodemailer
- Success popup notification
- Confirmation email to users
- Admin notification email to codotechit@gmail.com

## Changes Made

### 1. **Frontend Updates** (`app/page.js`)
- Added "Contact Us" link to navbar (desktop & mobile)
- Changed "Get Started Free" buttons to "Contact Us" with scroll to contact section
- Added full Contact Us section with:
  - Contact information display (email, phone, location, hours)
  - Responsive contact form
  - Success popup message

### 2. **Backend API** (`app/api/contact/route.js`)
- Created POST endpoint `/api/contact`
- Sends two emails:
  - Admin notification to codotechit@gmail.com
  - Confirmation email to user
- Validates form data
- Error handling

### 3. **Environment Variables** (`.env.local`)
- EMAIL_USER: Gmail account
- EMAIL_PASSWORD: Gmail App Password (NOT regular password)

## Setup Instructions

### Step 1: Get Gmail App Password
1. Go to: https://myaccount.google.com/apppasswords
2. Select "Mail" and "Windows Computer" (or your device)
3. Google will generate a 16-character password
4. Copy this password

### Step 2: Configure Environment Variables
1. Open `frontend/.env.local`
2. Replace `your_gmail_app_password_here` with the 16-character password from Step 1
3. Keep EMAIL_USER as: `codotechit@gmail.com`

Example:
```
EMAIL_USER=codotechit@gmail.com
EMAIL_PASSWORD=abcd efgh ijkl mnop
```

### Step 3: Test the Form
1. Navigate to the landing page
2. Click "Contact Us" button or scroll to contact section
3. Fill in the form:
   - Full Name (required)
   - Email (required)
   - Phone (optional)
   - Message (required)
4. Click "Send Message"
5. You should see a success popup
6. Check both:
   - codotechit@gmail.com (admin email)
   - Your email address (confirmation email)

## Features

### Contact Section Layout
- **Left Side**: Contact information with icons
  - Email: codotechit@gmail.com
  - Phone: +91 (123) 456-7890 (update as needed)
  - Location: New Delhi, India (update as needed)
  - Business Hours: Monday - Friday: 9AM - 6PM IST

- **Right Side**: Contact form
  - Full Name field (required)
  - Email field (required)
  - Phone field (optional)
  - Message textarea (required)
  - Submit button with loading state

### Success Experience
- After submission, form clears
- Success popup appears for 5 seconds
- Message: "Thank you for reaching out. Our team will get back to you soon!"

### Email Features
- **Admin Email**: Receives all form submissions with user details
- **User Email**: Receives confirmation that message was received
- Professional HTML formatted emails
- Error handling and feedback

## Customization

### Update Contact Information
Edit the Contact Info section in `app/page.js`:
```javascript
<p className="text-slate-600 dark:text-slate-400">+91 (123) 456-7890</p>  // Update phone
<p className="text-slate-600 dark:text-slate-400">New Delhi, India</p>     // Update location
```

### Update Email Addresses
In `.env.local`:
- Change `EMAIL_USER` if you want to use a different Gmail account
- Change the "to" email in `app/api/contact/route.js` if you want notifications to go elsewhere

### Styling
All form elements are styled with Tailwind CSS and support dark mode automatically.

## Troubleshooting

### "Failed to send message" error
1. Check environment variables are set correctly in `.env.local`
2. Verify Gmail App Password is correct (not regular password)
3. Ensure Gmail account is properly configured for app passwords
4. Check browser console for detailed error messages

### Emails not receiving
1. Verify EMAIL_USER and EMAIL_PASSWORD in `.env.local`
2. Check spam/junk folder
3. Confirm Gmail account allows "Less secure apps" if needed
4. Test with a simple form submission first

### Form not submitting
1. Check console for JavaScript errors
2. Verify `/api/contact` endpoint is accessible
3. Ensure all required fields are filled
4. Check network tab in browser dev tools

## Mobile Responsiveness
- Contact form is fully responsive
- Stacks vertically on mobile devices
- Form inputs are touch-friendly
- Success popup is mobile optimized

## Dark Mode
- All elements support light and dark mode
- Form styling adapts to theme automatically
- Success popup respects current theme

## Security Notes
- Form validates required fields
- Email addresses are validated
- Only necessary data is sent to backend
- Environment variables keep credentials secure
