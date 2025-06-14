# HW4: Rich Notes, XSS, and Web Security

## What is XSS?
Cross-Site Scripting (XSS) is a security vulnerability that allows attackers to inject malicious scripts into web pages viewed by other users. XSS can be exploited to steal information, hijack user sessions, or perform actions on behalf of users without their consent. This exercise demonstrates how adding rich text (HTML) support to a web app can introduce XSS vulnerabilities, and how to defend against them using sanitization.

## Overview
In this assignment, you will extend your previous note-taking web application to support rich text notes (with HTML formatting), explore XSS vulnerabilities, and implement defenses. You will:
- Implement a rich note feature that allows users to use HTML tags (e.g., `<b>`, `<i>`, `<img>`, etc.) in their notes.
- Demonstrate how this feature introduces an XSS vulnerability by injecting a keylogger payload.
- Build an attacker server that receives keystrokes from the keylogger.
- Implement a sanitizer to defend against XSS attacks.
- Add a radio button in the frontend to toggle the sanitizer on/off and visually demonstrate the difference.
- Write Playwright tests to verify both the vulnerable and protected behaviors.

## Submission
- Coding: 70%, Questions: 30%.
- Your submitted git repo should be *private*, please add 'barashd@post.bgu.ac.il', 'Gurevichronen@gmail.com', 'daninost', and 'Gal-Fadlon' to the list of collaborators.
- Deadline: 27.06.25, end of day.
- Additionally, solve the [thoretical questions](#TBD).
- Use TypeScript, and follow the linter's warnings (see eslint below).
- The ex4 forum is open for questions in Moodle. It's highly recommended to use it for design, technical issues, and any general subject.

- Git repository content:
  - Aim for a minimal repository size that can be cloned and installed: most of the files in github should be code and package dependencies (add package.json, index.html).
  - Don't submit (add to git) .env (it's your secret file which includes passwords- add to gitignore), node_modules dir, package-lock.json, or note json files.
  - the submission commit will be tagged as "submission_hw4" using the same github link as hw1. (See [git tagging](https://git-scm.com/book/en/v2/Git-Basics-Tagging))
  - to test your submission, run the presubmission script (in github). A submission that does not pass the presubmission script, gets a 0 score automatically.

## AI
Tip for using an AI Assistant: You can ask questions and read the answers, but avoid copying them. Understand the details but write the code yourself.

Requirements for AI usage:
- If you use an AI assistant (e.g., ChatGPT, Claude, etc.), you must share your conversation with the AI:
    - Use the "share" option provided by the AI tool to generate a link to the conversation.
    - If the tool does not have a "share" option, provide a PDF containing screenshots of the chat.
- Submit the shared conversation link or PDF along with your homework.
- You are expected to fully understand your own code, and be able to answer questions about it, frontally.
## Plagiarism
- We use a plagiarism detector.
- The person who copies and the person who was copied from are both responsible. Set your repository private, and don't share your code.
- If the code was copied from an AI agent, we expect it to appear in the shared conversation above.
- Exception: You can, and it's recommended, to share tests with other students, and share ideas and thoughts in the forum.

## Assignment Steps

### 1. Rich Notes & XSS Vulnerability
- Allow users to create notes with rich HTML content (e.g., `<b>`, `<i>`, `<img>`, etc.).
- Render note content using `dangerouslySetInnerHTML` (or equivalent), making the app intentionally XSS-vulnerable.
- Demonstrate the vulnerability by injecting a keylogger payload.
  - Implement a keylogger script that sends each keystoke to an attacker server.
  - Inject it in a new rich note. `Note: There are multiple ways to do so, some are blocked by the browers.  Find a way that works :)`

### 2. Attacker Server & Keylogger
- Implement a simple attacker server (Node.js recommended) that listens for POST requests and logs keystrokes to a file (e.g., `keylog.txt`).
- The keylogger payload in the note should send keystrokes to this server.

### 3. Sanitizer & Defense
- Implement a sanitizer function that removes dangerous tags/attributes (e.g., `<script>`, `onerror`, etc.) but allows safe formatting tags.
- Add a radio button in the frontend to toggle between sanitized and raw HTML rendering for notes.
- When sanitization is ON, XSS/keylogger should not work; when OFF, it should.

### 4. Testing
- Write Playwright tests to:
  - Verify rich text rendering (e.g., `<b>`, `<i>` tags are preserved).
  - Demonstrate XSS/keylogger works when sanitizer is OFF.
  - Demonstrate sanitizer blocks XSS when ON.
  - Cover CRUD operations as in previous assignments.

## Recommended Reading
- [MDN Web Docs: Cross-site scripting (XSS)](https://developer.mozilla.org/en-US/docs/Glossary/Cross-site_scripting)
- [OWASP XSS (Cross Site Scripting) Cheat Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Cross_Site_Scripting_Prevention_Cheat_Sheet.html)
- [DOMPurify (for reference, do not use in this assignment)](https://github.com/cure53/DOMPurify)
- [React docs: dangerouslySetInnerHTML](https://react.dev/reference/react-dom/components/common#dangerously-setting-the-inner-html)
- [Node.js HTTP server basics](https://nodejs.org/en/docs/guides/getting-started-guide)

## Example Directory Structure
```
.
├── backend
│   ├── ...
├── frontend
│   ├── src
│   │   ├── components
│   │   │   ├── Pagination.ts
│   │   │   ├── Post.tsx
│   │   │   ├── PostList.tsx
│   │   │   ├── sanitizeHtml.ts
│   │   │   ├── ...
│   │   ├── ...
│   ├── playwright-tests
│   │   ├── test.spec.ts
│   │   ├── ...
│   ├── ...
├── attacker_server.js
```

## Good luck!

