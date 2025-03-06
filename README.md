# OPNsense Theme
## Creating a custom theme for OPNsense involves modifying the frontend assets (CSS, images, etc.) and integrating it into the OPNsense framework. Below is a step-by-step guide:

---

### **1. Understand the OPNsense Theme Structure**
- OPNsense uses **Bootstrap 4** for its UI, so familiarity with Bootstrap theming is helpful.
- Themes are located in `/usr/local/opnsense/www/themes/` (or `src/www/themes` in the [GitHub repo](https://github.com/opnsense/opnsense)).
- Core themes include:
  - `opnsense.css` (default theme)
  - `dark-theme.css`
  - `light-theme.css`

---

### **2. Create a New Theme Directory**
1. **Clone the OPNsense repo** or navigate to the themes directory:
   ```bash
   git clone https://github.com/opnsense/core.git
   cd core/src/www/themes
   ```

2. **Create a new folder** for your theme, e.g., `custom-theme`.

3. **Add required files**:
   - `custom-theme.css` (main stylesheet)
   - `info.xml` (metadata)
   - Optional: Images, fonts, or JS overrides.

---

### **3. Define Theme Metadata (`info.xml`)**
Example `info.xml`:
```xml
<?xml version="1.0"?>
<theme>
  <name>custom-theme</name>
  <description>My Custom OPNsense Theme</description>
  <version>1.0</version>
  <author>Your Name</author>
  <licence>BSD-2-Clause</licence>
</theme>
```

---

### **4. Customize Styles**
- Override Bootstrap variables or OPNsense-specific classes in `custom-theme.css`.
- Example:
  ```css
  /* Override primary color */
  :root {
    --primary: #ff5722;
  }

  /* Custom navbar styling */
  .navbar {
    background-color: var(--primary) !important;
  }
  ```
- Use the OPNsense default theme ([opnsense.css](https://github.com/opnsense/core/blob/master/src/www/themes/opnsense/build/css/opnsense.css)) as a reference.

---

### **5. Integrate the Theme into OPNsense**
1. **Copy your theme** to the OPNsense server:
   ```bash
   scp -r custom-theme root@firewall:/usr/local/opnsense/www/themes/
   ```

2. **Enable the theme** in the OPNsense GUI:
   - Go to **System > Settings > General**.
   - Select your theme under **Theme**.

---

### **6. Test and Debug**
- Use browser developer tools (F12) to inspect elements and test responsiveness.
- Clear your browser cache after updates.

---

### **7. Package the Theme (Optional)**
To share your theme:
1. Create a **plugin** or submit a pull request to the [OPNsense plugins repo](https://github.com/opnsense/plugins).
2. Include a `Makefile` for installation:
   ```makefile
   PLUGIN_NAME=    theme-custom
   PLUGIN_VERSION= 1.0
   PLUGIN_COMMENT= My Custom Theme
   PLUGIN_MAINTAINER= you@example.com
   ```

---

### **Example Custom Theme Repo**
Check existing community themes like:
- [OPNsense Dark Theme](https://github.com/opnsense/plugins/tree/master/www/theme-vicuna)
- [OPNsense Material Theme](https://github.com/neonfuture/OPNsense-Theme)

---

### **Troubleshooting**
- If the theme doesn’t appear, check permissions: `chmod -R 755 /usr/local/opnsense/www/themes/custom-theme`.
- Validate CSS syntax using tools like [CSS Linter](https://stylelint.io/).

---

By following these steps, you can create and deploy a fully custom OPNsense theme. For advanced changes, study the [OPNsense MVC architecture](https://docs.opnsense.org/development.html).
