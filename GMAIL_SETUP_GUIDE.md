# Gmail Setup Guide for Contact Form

## Important: Fix the "Failed to send message" Error

The error occurs because Gmail credentials are not properly configured. Follow these steps carefully:

## Step 1: Enable 2-Factor Authentication on Gmail

1. Go to: https://myaccount.google.com/security
2. Look for "2-Step Verification" section
3. Click on it and follow the setup process
4. You must enable this BEFORE you can generate App Passwords

## Step 2: Generate Gmail App Password

1. Go to: https://myaccount.google.com/apppasswords
2. You should see a dropdown that says "Select the app and device you're using"
3. Select "Mail" from the dropdown
4. Select "Windows Computer" (or your operating system)
5. Click "Generate"
6. Google will display a 16-character password (looks like: `abcd efgh ijkl mnop`)
7. **Copy this password** - you'll need it in the next step

## Step 3: Update Your Environment Variables

1. Open the file: `frontend/.env.local`
2. Update with your credentials:

```
EMAIL_USER=codotechit@gmail.com
EMAIL_PASSWORD=abcd efgh ijkl mnop
```

**Important:**
- Replace `abcd efgh ijkl mnop` with the actual 16-character password from Step 2
- Keep the spaces in the password exactly as Google provided it
- Do NOT use your regular Gmail password
- Do NOT remove the `.env.local` file

## Step 4: Restart Your Development Server

1. Stop your dev server (Ctrl+C in terminal)
2. Start it again: `npm run dev`
3. Wait for it to fully load

## Step 5: Test the Contact Form

1. Navigate to your landing page
2. Scroll to the "Contact Us" section
3. Fill in the form:
   - **Full Name:** Your name (required)
   - **Email:** Your email (required)
   - **Phone:** Your phone number (required) ← Now required
   - **Message:** Optional message
4. Click "Send Message"
5. You should see a success popup

## Step 6: Verify Emails

Check both:
- **Your email inbox** - for confirmation email from myShop
- **codotechit@gmail.com inbox** - for admin notification

## Troubleshooting

### Still Getting "Failed to send message" Error?

**Check 1: Verify Environment Variables**
```bash
# Add this to frontend/.env.local to test:
EMAIL_USER=codotechit@gmail.com
EMAIL_PASSWORD=your_16_character_password_here
```

**Check 2: Ensure 2-Factor Authentication is Enabled**
- Go to https://myaccount.google.com/security
- Look for "2-Step Verification" - it should show "On"
- If it's "Off", enable it first

**Check 3: Look at Console Logs**
- Open browser DevTools (F12)
- Go to Console tab
- Look for error messages
- Take note of what it says

**Check 4: Check Terminal Output**
- Look at your terminal where dev server is running
- You should see console.log messages like:
  ```
  Sending admin email to: codotechit@gmail.com
  Admin email sent successfully
  Sending confirmation email to: user@example.com
  Confirmation email sent successfully
  ```

**Check 5: App Password Format**
- Gmail App Passwords have spaces: `abcd efgh ijkl mnop`
- Don't remove the spaces!
- Should be exactly 16 characters (including spaces)

**Check 6: Less Secure Apps (if using older Gmail accounts)**
- Go to https://myaccount.google.com/lesssecureapps
- If available, you may need to enable "Allow less secure apps"
- (This option may not appear in newer Google accounts)

## Gmail Account Requirements

For the contact form to work, your Gmail account must:
✅ Have 2-Step Verification enabled
✅ Have an App Password generated
✅ Have the App Password set in `.env.local`
✅ Be using the correct format in environment variables

## Security Notes

- Never commit `.env.local` to git (it should be in `.gitignore`)
- App Passwords are different from your regular Gmail password
- App Passwords can be revoked at any time from your Google account
- Each App Password is unique to your device/app

## Field Requirements - Updated

**Form Fields:**
- ✅ Full Name - **REQUIRED**
- ✅ Email - **REQUIRED**
- ✅ Phone - **REQUIRED** (changed from optional)
- ✅ Message - **OPTIONAL** (changed from required)

## Contact Information in Form

**Left Side - Contact Info:**
- Email: codotechit@gmail.com
- Phone: +91 (123) 456-7890 (update this in page.js)
- Location: New Delhi, India (update this in page.js)
- Business Hours: Monday - Friday: 9AM - 6PM IST (update this in page.js)

## Success Experience

When a user submits the form successfully:
1. ✅ Success popup appears
2. ✅ Form clears
3. ✅ Admin receives email
4. ✅ User receives confirmation email
5. ✅ Popup shows for 5 seconds then disappears

## Common Mistakes to Avoid

❌ Using your regular Gmail password instead of App Password
❌ Not enabling 2-Step Verification first
❌ Missing spaces in App Password (should be: `abcd efgh ijkl mnop`)
❌ Forgetting to restart dev server after updating .env.local
❌ Committing .env.local to version control
❌ Using an outdated App Password

## Still Not Working?

1. Double-check all steps above
2. Generate a NEW App Password and try again
3. Make sure you're using `codotechit@gmail.com` as EMAIL_USER
4. Verify no typos in `.env.local`
5. Check if Gmail account is locked (go to myaccount.google.com/security)
6. Try from a different browser/incognito mode
7. Contact Google support if your account is restricted

## Advanced: Custom Email Address

To send from a different email or send to a different admin email:

1. Change `EMAIL_USER` in `.env.local` to your email
2. Update the `to` field in `app/api/contact/route.js`
3. Look for: `const adminEmail = 'codotechit@gmail.com';`
4. Change it to your preferred email
5. Restart dev server
