# Little Hope Play School - Contact Form Setup Guide

This guide will help you configure the contact form to receive inquiries via email.

## Step 1: Create EmailJS Account

1. Go to [EmailJS](https://www.emailjs.com/) (it's free for up to 200 emails/month)
2. Click "Sign Up" and create an account using Google or email

## Step 2: Create an Email Service

1. After logging in, go to **Email Services** in the sidebar
2. Click **Add New Service** and select **Gmail** (recommended) or any other email provider
3. Follow the prompts to connect your email (e.g., littlehopeplayschool@gmail.com)
4. Note down your **Service ID** (it will look like: `service_xxxxxxx`)

## Step 3: Create an Email Template

1. Go to **Email Templates** in the sidebar
2. Click **Create New Template**
3. Use this template structure:

**Template Subject:** New Inquiry from Little Hope Website

**Template Body:**
```
New Admission Inquiry

Name: {{from_name}}
Email: {{from_email}}
Phone: {{phone}}
Child's Age: {{child_age}}
Preferred Tour Date: {{tour_date}}

Message:
{{message}}

---
This inquiry was submitted through the Little Hope Play School website.
```

4. Note down your **Template ID** (it will look like: `template_xxxxxxx`)

## Step 4: Get Your Public Key

1. Go to **Account** > **API Keys** (or click the gear icon)
2. Copy your **Public Key** (it will look like: `xxxxxx...`)

## Step 5: Update the Website Files

### Update `js/script.js`:

1. Open `js/script.js` in the school_website folder
2. Replace the placeholders with your actual IDs:

```javascript
// Around line 94-96, replace:
emailjs.init('YOUR_PUBLIC_KEY');

// With your actual public key, for example:
// emailjs.init('abcdefghijk123456789');
```

3. In the same file, around line 105, replace:

```javascript
emailjs.send('YOUR_SERVICE_ID', 'YOUR_TEMPLATE_ID', templateParams)
```

With your actual IDs, for example:
```javascript
emailjs.send('service_abc123', 'template_xyz789', templateParams)
```

### Update `contact.html`:

1. Open `contact.html` in the school_website folder
2. Around line 9, replace `YOUR_PUBLIC_KEY` with your actual public key:

```html
<script src="https://cdn.jsdelivr.net/npm/@emailjs/browser@4/dist/email.min.js"></script>
<script>
    // Add this line right after the EmailJS script, with your actual public key:
    (function() {
        emailjs.init('YOUR_ACTUAL_PUBLIC_KEY');
    })();
</script>
```

## Step 6: Test the Form

1. Open `contact.html` in your browser
2. Fill out the form with test data
3. Click "Send Inquiry & Book Tour"
4. Check your email for the test message

## Alternative: WhatsApp Integration

If you prefer getting inquiries as WhatsApp messages instead of email:

1. Create a free [formspree.io](https://formspree.io/) account
2. Get your form endpoint
3. Update the form action in `contact.html`:

```html
<form action="https://formspree.io/f/YOUR_FORM_ID" method="POST">
```

This will send form submissions directly to your email without any server setup.

## Support

If you need help:
- EmailJS Documentation: https://www.emailjs.com/docs/
- EmailJS Support: support@emailjs.com

## Cost

- **EmailJS Free Plan**: 200 emails/month (sufficient for a small school)
- **EmailJS Starter**: $15/month for 1000 emails/month