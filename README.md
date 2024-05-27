# Node.js M-Pesa Integration

## Overview
This project demonstrates integrating M-Pesa's STK push functionality with a Node.js server using Express.

## Project Structure
- **index.ts**: Sets up the Express app, configures middleware, defines routes, and starts the server.
- **controllers/stkController.ts**: Contains `handleStkPush` to handle M-Pesa STK push requests.
- **middlewares/generateToken.ts**: Defines `generateToken` to get an OAuth token from Safaricom and attaches it to the request.
- **routes/lipaRoute.ts**: Defines the `/stkpush` route using `generateToken` middleware and `handleStkPush` controller.

## Setup
1. Clone the repository.
2. Install dependencies:
   ```sh
   npm install

## Create a .env file with your M-Pesa credentials:
```
PORT=5000
MPESA_CONSUMER_KEY=your_consumer_key
MPESA_CONSUMER_SECRET=your_consumer_secret
MPESA_BUSINESS_SHORT_CODE=your_business_short_code
MPESA_PASS_KEY=your_pass_key
```
## Run the server:
```
npm start
```

## Endpoints
- GET /: Returns a welcome message.
- POST /lipa/stkpush: Initiates an M-Pesa STK push.

## Example Request
```sh
curl -X POST http://localhost:5000/lipa/stkpush \
  -H "Content-Type: application/json" \
  -d '{"phone": "2547XXXXXXXX", "amount": "10"}'
```

### Code Explanation

#### index.ts:

- Sets up the Express app.
- Configures middleware (express.json(), cors()).
- Defines a root route (/) and includes the /lipa route.
- Starts the server.

#### controllers/stkController.ts:

- Contains handleStkPush to handle M-Pesa STK push requests.
- Constructs the payload and sends a request to Safaricom's API using axios.

#### middlewares/generateToken.ts:

- Defines generateToken to get an OAuth token from Safaricom.
- Attaches the token to the request object.

#### routes/lipaRoute.ts:

- Defines the /stkpush route.
- Uses `generateToken` middleware and `handleStkPush` controller.

### Example Flow
- Client sends POST request to /lipa/stkpush.
- `generateToken` middleware:
  - Requests an OAuth token from Safaricom.
  - Adds the token to the request.
- `handleStkPush` controller:
  - Constructs the STK push payload.
  - Sends it to Safaricom's M-Pesa API.
  - Returns the response to the client.


