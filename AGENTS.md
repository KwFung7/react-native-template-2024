# Pet Health Project - Developer Guide

This document provides essential information for AI agents and developers working on the Pet Health React Native application.

## 1. Build, Lint, and Test Commands

### Build & Run

- **Install Dependencies:** `yarn install` (Prefer Yarn over NPM)
- **iOS (Dev):** `yarn ios:dev` (Simulator: iPhone 17 Pro)
- **Android (Dev):** `yarn android:dev`
- **Start Metro Bundler:** `yarn start:dev` (includes cache reset)
- **Clean Cache:** `yarn clean:cache` (Useful for resolving build issues)

### Testing

- **Run All Tests:** `yarn test`
- **Run Single Test File:** `npx jest path/to/testFile.test.ts`
- **Run Specific Test Case:** `npx jest path/to/testFile.test.ts -t "test name pattern"`

### Linting

- **Run Lint:** `yarn lint` (Uses ESLint)

## 2. Project Structure

The source code is located in `src/app/`.

- `actions/`: Redux action creators.
- `api/`: API integration (Axios wrappers).
- `component/`: Reusable "dumb" components.
- `constant/`: Constants (Colors, Strings).
- `container/`: "Smart" components / Screens connected to Redux.
- `navigator/`: React Navigation configuration.
- `reducers/`: Redux reducers.
- `store/`: Redux store configuration.
- `util/`: Utility functions.

## 3. Code Style & Conventions

### General

- **Language:** TypeScript.
- **Indentation:** 2 spaces.
- **Quotes:** Single quotes `'` preferred.
- **Semicolons:** Always use semicolons.

### Naming Conventions

- **Directories:** camelCase (e.g., `src/app/component/regularTextInput`).
- **Files:** camelCase for logic, PascalCase for top-level component files often mapped to `index.ts`.
- **Components:** PascalCase (e.g., `RegularTextInput`).
- **Interfaces/Types:** PascalCase (e.g., `RegularTextInputProps`).
- **Variables/Functions:** camelCase (e.g., `handleFocus`).
- **Constants:** UPPER_SNAKE_CASE (e.g., `COLOR.SLATE_GRAY`).

### Component Structure

- Use **Functional Components** with `React.FC`.
- Define `Props` interface immediately before the component.
- Destructure props in the function signature.
- **Styling:** Use `styled-components/native`.
  - Define styles in a separate `style.ts` file in the same directory.
  - Export styled components and import them in `index.tsx`.
- **Imports:**
  1. React and React Native.
  2. Third-party libraries.
  3. Internal components/constants (Relative paths).
  4. Styles.

#### Example Component (`index.tsx`):

```tsx
import React from 'react';
import {View} from 'react-native';
import {StyledText} from './style';

interface MyComponentProps {
  title: string;
}

const MyComponent: React.FC<MyComponentProps> = ({title}) => {
  return (
    <View>
      <StyledText>{title}</StyledText>
    </View>
  );
};

export default MyComponent;
```

#### Example Style (`style.ts`):

```ts
import styled from 'styled-components/native';
import COLOR from '../../constant/color';

export const StyledText = styled.Text`
  font-size: 16px;
  color: ${COLOR.BLACK};
`;
```

### State Management (Redux)

- **Pattern:** Legacy Redux (Actions, Reducers, Types).
- **Actions:** Define action types as string constants in `type.ts`. Create action creators in `actions/`.
- **Reducers:** specific reducers handling state updates based on action types.

### Networking

- Use the `src/app/api/` abstractions.
- Do not use `axios` directly in components; use the helper functions defined in `api/`.

### Error Handling

- Use `try/catch` blocks for async operations.
- API errors are typically caught in the promise chain or async wrapper.

## 4. Environment Variables

- Environment specific configurations are managed via `.env` files (e.g., `.env.dev`, `.env.uat`, `.env.prod`).
- Use `react-native-config` to access them.
