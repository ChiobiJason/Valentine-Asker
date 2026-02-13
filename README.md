# Valentine Asker

A cute Vue.js application to ask your special someone to be your valentine! Features a photo carousel, love quotes, and an interactive "Yes/No" question where the "No" button is hard to resist (because the "Yes" button keeps growing!).


This template should help get you started developing with Vue 3 in Vite.

## Setup Instructions

### 1. Install Dependencies
```sh
npm install
```

### 2. Environment Variables
Create a `.env` file in the root directory and add your EmailJS configuration. Use the `APP_` prefix as required by our custom Vite config.

```env
APP_EMAILJS_SERVICE_ID=your_service_id
APP_EMAILJS_TEMPLATE_ID=your_template_id_for_you
APP_EMAILJS_TEMPLATE_ID_CONFIRMATION=your_template_id_for_partner
APP_EMAILJS_PUBLIC_KEY=your_public_key
APP_EMAIL_TO_JASON=your_email@example.com
APP_EMAIL_TO_EFFIE=partner_email@example.com
```

### 3. EmailJS Setup
- Create an account on [EmailJS](https://www.emailjs.com/).
- Create two templates:
    1.  **Notification Template (for you)**: Uses variables `{{to_name}}`, `{{from_name}}`, `{{message}}`, `{{email}}`.
    2.  **Confirmation Template (for partner)**: Uses `{{to_name}}`, `{{from_name}}`, `{{message}}`.
- HTML templates are provided in `email_template.html` and `email_template_confirmation.html`.


## Project Setup

```sh
npm install
```

### Compile and Hot-Reload for Development

```sh
npm run dev
```

### Compile and Minify for Production

```sh
npm run build
```
