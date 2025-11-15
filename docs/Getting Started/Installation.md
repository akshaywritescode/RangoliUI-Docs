---
sidebar_position: 1
---

# Installation
Rangoli does not require any additional libraries or tools, you just need to copy & paste component code. Since it is based on shadcn, make sure you have shadcn installed. For more details, visit the [Shadcn Installation Documentation](https://ui.shadcn.com/docs/installation)

## Make Sure Dependencies
If you have already installed shadcn, ensure that your `package.json` includes the following dependencies, either under `devDependencies` or `dependencies`. If any are missing, you can install them manually.

```json
  "dependencies": {
    "@radix-ui/react-dialog": "^1.1.15",
    "@radix-ui/react-popover": "^1.1.15",
    "@radix-ui/react-slot": "^1.2.4",
    "class-variance-authority": "^0.7.1",
    "clsx": "^2.1.1",
    "cmdk": "^1.1.1",
    "lucide-react": "^0.553.0",
    "next": "16.0.3",
    "react": "19.2.0",
    "react-dom": "19.2.0",
    "tailwind-merge": "^3.4.0"
  },
  "devDependencies": {
    "@tailwindcss/postcss": "^4",
    "@types/node": "^20",
    "@types/react": "^19",
    "@types/react-dom": "^19",
    "eslint": "^9",
    "eslint-config-next": "16.0.3",
    "tailwindcss": "^4",
    "tw-animate-css": "^1.4.0",
    "typescript": "^5"
  }
```