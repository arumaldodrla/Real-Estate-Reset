# Internationalization (i18n) Specification

This document outlines the strategy and technical implementation for the internationalization (i18n) of the frontend application. The goal is to create a robust system that supports multiple languages, starting with English and Spanish, and can be easily extended with the help of AI.

## 1. i18n Framework

- **Framework:** `i18next` will be used as the core i18n framework for the React frontend.
- **React Integration:** `react-i18next` will be used for seamless integration with React components.

## 2. Language & Namespace Structure

- **Default Language:** English (`en`)
- **Initial Translation:** Spanish (`es`)
- **File Structure:** Translation files will be organized by language and namespace in the `frontend/public/locales` directory.

```
/public
  /locales
    /en
      common.json
      transactions.json
      crm.json
    /es
      common.json
      transactions.json
      crm.json
```

- **Namespaces:**
  - `common`: Shared translations (buttons, labels, etc.)
  - `transactions`: Translations specific to the transaction management module.
  - `crm`: Translations specific to the CRM module.

## 3. AI-Assisted Translation Workflow

To accelerate the translation process for future languages, we will implement an AI-assisted workflow:

1.  **Source File Generation:** A script will be created to extract all the English translation keys and values from the `en` directory into a single source file.
2.  **AI Translation:** This source file will be fed to an LLM (e.g., Gemini) with a prompt to translate the values to the target language, maintaining the JSON structure.
3.  **File Creation:** The AI-generated output will be used to create the new language files (e.g., `/fr/common.json`).
4.  **Human Review:** A human reviewer will then validate the AI-generated translations for accuracy and cultural context.

## 4. Implementation in React Components

All user-facing strings in the React components must be replaced with the `t` function from the `useTranslation` hook.

**Example:**

```jsx
import { useTranslation } from 'react-i18next';

const MyComponent = () => {
  const { t } = useTranslation('transactions');

  return (
    <div>
      <h1>{t('title')}</h1>
      <p>{t('description')}</p>
    </div>
  );
};
```

## 5. Language Selection UI

A language selector component will be added to the application's header or settings page, allowing users to switch between supported languages.
