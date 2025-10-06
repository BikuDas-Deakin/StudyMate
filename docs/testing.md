# StudyMate - Testing Documentation

> End-to-end and API testing guide for StudyMate collaborative study platform.

## Testing Stack

- **E2E Testing:** Cypress
- **Unit Testing:** Jest
- **Coverage Target:** ≥85%

## Setup

### Install Dependencies

```bash
npm install --save-dev cypress jest
npx cypress verify
```

### Environment Configuration

Create `cypress.env.json`:

```json
{
  "apiUrl": "http://localhost:5000",
  "testUser": {
    "email": "jane@example.com",
    "password": "secret123"
  }
}
```

**Note:** Add `cypress.env.json` to `.gitignore`

## Test Structure

```
cypress/
├── e2e/
│   ├── 1-getting-started/      # Cypress examples
│   ├── 2-advanced-examples/    # Cypress examples
│   ├── auth.cy.js              # Auth API tests
│   ├── auth.e2e.cy.js          # Auth E2E flow
│   ├── chat.cy.js              # Chat API tests
│   ├── dashboard.cy.js         # Dashboard API tests
│   ├── dashboard.e2e.cy.js     # Dashboard E2E tests
│   ├── room-chat.e2e.cy.js     # Room & chat E2E
│   ├── rooms.cy.js             # Rooms API tests
│   ├── rooms.e2e.cy.js         # Rooms E2E tests
│   ├── smoke.cy.js             # Smoke tests
│   └── users.cy.js             # Users API tests
├── support/
│   ├── commands.js             # Custom commands
│   └── e2e.js
└── fixtures/
```

## Test Categories

### 1. API Tests

#### Authentication (`auth.cy.js`)
- Valid login returns JWT
- Invalid credentials rejected (400/401)
- JWT format validation

#### Rooms (`rooms.cy.js`)
- List all accessible rooms
- Create new room
- Fetch room by ID

#### Dashboard (`dashboard.cy.js`)
- Dashboard API integration
- Room listing data

#### Chat (`chat.cy.js`)
- Post message to room
- Fetch room messages
- Reject empty messages

#### Users (`users.cy.js`)
- User list from fixtures
- User data validation

### 2. E2E Tests

#### Auth Flow (`auth.e2e.cy.js`)
- Login via UI
- Token persistence
- Dashboard redirect

#### Rooms E2E (`rooms.e2e.cy.js`)
- Room creation flow
- Room navigation
- Room interactions

#### Dashboard E2E (`dashboard.e2e.cy.js`)
- Load and render rooms
- Navigate to room
- Create room button
- Handle API errors

#### Room & Chat E2E (`room-chat.e2e.cy.js`)
- Create room via API
- Open room page
- Send message via UI
- Verify message appears (Socket.io)

#### Smoke Tests (`smoke.cy.js`)
- Server reachability
- Public pages load
- Protected pages redirect
- Room page with auth

## Custom Commands

### Authentication

```javascript
// Login and return token
cy.apiLogin(email, password)

// Login and store token in localStorage
cy.loginByApi(email, password)

// Make authenticated request
cy.authRequest({ method: 'GET', url: '/api/rooms' })
```

### Room Management

```javascript
// Create room and return ID
cy.createRoom('Room Name').then(({ id }) => {
  // use room id
})
```

## Running Tests

```bash
# Run all tests (headless)
npx cypress run

# Open Cypress UI
npx cypress open

# Run specific suite
npx cypress run --spec "cypress/e2e/smoke.cy.js"

# Run API tests only
npx cypress run --spec "cypress/e2e/{auth,rooms,chat,dashboard,users}.cy.js"

# Run E2E tests only
npx cypress run --spec "cypress/e2e/*.e2e.cy.js"

# Run with specific browser
npx cypress run --browser chrome

# Jest unit tests
npm test
npm test -- --watch
npm test -- --coverage
```

## Best Practices

### Flexible Selectors
Use multiple selector strategies for robustness:
```javascript
cy.get('#messageInput, [data-cy="message-input"]').type('Hello')
```

### Error Handling
Expect and handle errors explicitly:
```javascript
cy.request({
  url: '/api/rooms',
  failOnStatusCode: false
}).then((resp) => {
  expect([400, 422]).to.include(resp.status)
})
```

### Test Isolation
Each test should be independent:
```javascript
beforeEach(() => {
  cy.visit('/login.html')
  cy.loginByApi(email, password)
})
```

### Stub External Services
Prevent Socket.io from breaking tests:
```javascript
before(() => {
  cy.intercept('GET', '/socket.io/**', { statusCode: 200 })
  cy.intercept('POST', '/socket.io/**', { statusCode: 200 })
})
```

## Troubleshooting

**Timeout errors:** Increase timeout in `cypress.config.js`:
```javascript
defaultCommandTimeout: 10000
```

**Token not persisting:** Store in multiple localStorage keys:
```javascript
['token', 'accessToken', 'jwt'].forEach(k => 
  win.localStorage.setItem(k, token)
)
```

**Room URL errors:** Try both `?roomId=` and `?id=` parameters

**Socket.io errors:** Stub requests in smoke tests (see above)

## Configuration Files

### cypress.config.js
```javascript
module.exports = {
  e2e: {
    baseUrl: 'http://localhost:5000',
    supportFile: 'cypress/support/e2e.js',
    video: false,
    defaultCommandTimeout: 10000
  }
}
```

### jest.config.js
```javascript
module.exports = {
  testEnvironment: 'node',
  coverageThreshold: {
    global: {
      branches: 85,
      functions: 85,
      lines: 85
    }
  }
}
```

## Coverage Reports

Generate coverage report:
```bash
npm test -- --coverage
open coverage/lcov-report/index.html
```

---

**Last Updated:** October 2025
