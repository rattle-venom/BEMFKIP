---

## Security Analysis & Case Study

As an aspiring cybersecurity professional, I built this project with security in mind and analyzed it for potential vulnerabilities and mitigations.

### 1. Authentication & Authorization
- **Authentication:** The application uses **Firebase Authentication** to manage administrator access. The `admin.html` page and dashboard functionalities are only accessible to logged-in users.
- **Authorization (The Core Defense):** The true security of the database relies on **Firebase Security Rules**. These server-side rules are the ultimate authority on who can access data. For this project, the rules are configured to allow public read-access for news and gallery items, while write/delete permissions are strictly limited to authenticated administrators. This prevents unauthorized database access, even if the public-facing API keys are known.

### 2. Web Application Security
- **Cross-Site Scripting (XSS) Prevention:** To prevent stored XSS attacks from content entered in the news editor, I implemented a `sanitizeHTML` function in the `news-detail.html` page. This function encodes HTML characters from the database content before it is rendered on the page, ensuring that any malicious scripts are not executed by the browser.
- **Secure Form Endpoint:** The public contact form in `kontak.html` uses **Formspree**, a secure third-party service. This mitigates the risk of server-side vulnerabilities (like mail command injection) by offloading the email handling process to a trusted provider.

### 3. Secure Deployment & Configuration
- **HTTPS Enforcement:** The site is deployed on Vercel, which automatically enforces HTTPS. This encrypts all traffic, protecting against man-in-the-middle (MitM) attacks.
- **Environment Variables (Best Practice):** While Firebase API keys are designed to be public, the best practice for managing secrets is using environment variables. This prevents keys from being hardcoded in the source code and tracked in version control. In a future iteration, I would integrate a build step to manage these keys through Vercel's Environment Variables service.
