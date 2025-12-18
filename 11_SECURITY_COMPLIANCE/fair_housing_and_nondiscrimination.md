# Fair Housing and Nondiscrimination Policy

This document outlines the platform's commitment to fair housing and nondiscrimination, and the technical and policy controls in place to uphold these principles, particularly within the AI Property Agent.

## 1. Legal Framework

The platform is designed to comply with the Fair Housing Act in the United States and similar nondiscrimination laws in other jurisdictions. These laws prohibit discrimination in housing based on race, color, religion, sex, national origin, disability, or familial status.

## 2. AI Chatbot Guardrails

The AI Property Agent is built with strong guardrails to prevent discriminatory behavior:

- **No Asking for Protected Characteristics**: The chatbot will never ask a user for information about their protected characteristics.
- **Ignoring Protected Characteristics**: If a user volunteers information about their protected characteristics, the chatbot will ignore this information in its property recommendations.
- **Neutral Language**: The chatbot will use neutral and objective language when describing properties and neighborhoods.
- **Refusal to Answer Inappropriate Questions**: If a user asks a question that could lead to a fair housing violation (e.g., "Is this a good neighborhood for families?"), the chatbot will refuse to answer directly and will instead provide objective information about the property itself. The prompt library contains specific refusal patterns for such scenarios.

## 3. Regular Auditing and Testing

- **Conversation Audits**: A random sample of chatbot conversations will be audited regularly to check for any signs of bias or discrimination.
- **Red Teaming**: The AI model will be subject to "red teaming" exercises, where testers will attempt to elicit discriminatory responses from the chatbot. The results of these tests will be used to improve the AI's guardrails.

## 4. Training and Awareness

While the AI agents will be executing the development, the principles of fair housing and nondiscrimination are a core part of the requirements and will be embedded in the acceptance criteria for all related features.
