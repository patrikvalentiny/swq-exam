---
marp: true
theme: default
paginate: true
backgroundColor: #f0f4f8
style: |
  section {
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
  }
  h1 {
    color: #2c3e50;
  }
  h2 {
    color: #34495e;
  }
  code {
    background-color: #e0e0e0;
    padding: 2px 5px;
    border-radius: 4px;
  }
---

# Comparison of IDEs For Exploring and Testing APIs

## Postman vs. Insomnia vs. Bruno

Patrik Valentiny

---

## Project Overview

Evaluate and compare Integrated Development Environments (IDEs) for API testing.

**The Contenders:**

- **Postman:** The Industry Standard.
- **Insomnia:** The Extensible Alternative.
- **Bruno:** The Local-First Option.

---

## Context: Agile Testing

### How these tools map to Agile Testing Quadrants

- **Q1 (Tech-facing/Team-support):** Automated integration tests via API calls.
- **Q2 (Business-facing/Team-support):** Functional API tests.
- **Q4 (Tech-facing/Product-critique):** Performance and security checks.

---

## Test techniques used in API Testing

### Test Design Techniques (White-Box)

- **Integration Tests:** Validate the whole system via API endpoints.
- **Data-Driven Tests:** Using test data to validate API responses.
  
### Test Design Techniques (Black-Box)

- **Equivalence Class Testing:** Test various input categories (e.g., valid/invalid IDs).
- **Boundary Value Analysis:** Test API limits (e.g., limit, offset).

---

## Verification vs. Validation

- **Verification ("Building it right"):**
  - Automated tests confirm that specifications are met.
- **Validation ("Building the right product"):**
  - Manual exploration (Q3) within the IDE allows developers to "feel" the data.

---

## Tool comparison methodology

The comparison evaluates the tools across five key dimensions:

1. **Performance:** Overall tool responsiveness.
2. **Maintainability:** Organisation, environment setup, and Git/versioning support.
3. **Security:** Local vs. Cloud storage of credentials and environment variables.
4. **Testing Capabilities:** Assertions, scripting framework, and reporting.
5. **Extra Features:** Mock servers, collaboration tools, and automation capabilities.

---

## Performance

- **Postman:** Notably slow startup and UI responsiveness.
- **Insomnia:** Moderate performance, but can lag with large collections.
- **Bruno:** Fast startup and snappy UI, optimized for local use.

---

## Maintainability

- **Postman:** Uses proprietary format; possible to export to JSON.
- **Insomnia:** Supports JSON/YAML exports; has a plugin ecosystem.
- **Bruno:** Git-native; collections stored as code (`.bru`), ideal for CI/CD.

---

## Security

- **Postman:** Cloud-first; sensitive data are stored on Postman servers if user opts in.
- **Insomnia:** Recently shifted to cloud-first; local storage available but less emphasized.
- **Bruno:** Offline-only; all data stored locally, ensuring maximum privacy. (Git integration poses a risk if not managed properly.)
  
---

## Testing Capabilities

All three tools use JavaScript with Chai assertions for scripting post-request tests.

- **Postman:** Includes a rich set of built-in assertions and reporting features.
- **Insomnia:** Good scripting support; reporting is basic.
- **Bruno:** Separate tab for tests; supports no-code assertions. Reporting is also basic.

---

## Extra Features

- **Postman:** Extensive features including Mock Servers, AI assistance, and team collaboration.
- **Insomnia:** Plugin ecosystem, design-focused features.
- **Bruno:** Developer-centric features; lacks cloud collaboration but excels in local development.

---

## Comparison Summary

### Postman (The Enterprise Suite)

- **Strengths:** Rich feature set, Mock Servers, AI assistance.
- **Weaknesses:** Bloated, Slow, Forced Cloud Sync.

### Insomnia (The Middle Ground)

- **Strengths:** Design, Plugin Ecosystem.
- **Weaknesses:** Recent shift to cloud-first, unstable CLI.

### Bruno (The Developer Tool)

- **Strengths:** Speed, Offline-only, Git-Native, Privacy.
- **Weaknesses:** Newer ecosystem, fewer "cloud" collaboration features.
