# AcadPay - School Payment System

A robust school payment management system built with NestJS, providing secure and efficient payment processing for educational institutions.

## Features

- User Authentication and Authorization
- Comprehensive Payment Processing
- Transaction Management
- Payment Status Tracking
- Webhook Integration
- School-specific Transaction Views

## Prerequisites

Before you begin, ensure you have the following installed:
- Node.js (v18 or higher)
- npm (v9 or higher)
- Nest CLI (v11 or higher) (`npm install -g @nestjs/cli`)
- MongoDB (v6.0 or higher)

## Installation

1. Clone the repository:
```bash
git clone https://github.com/Abhiishekk31/AcadPay-backend.git
cd acadpay
```

2. Install dependencies:
```bash
npm install
```

3. Set up environment variables:
Create a `.env` file in the root directory and add the following variables:

```env
# Server Configuration
PORT=3000
NODE_ENV=development

# Database Configuration
MONGODB_URI=mongodb://localhost:27017/acadpay

# JWT Configuration
JWT_SECRET=your_jwt_secret_key
JWT_EXPIRATION=24h

# Payment Gateway Configuration
PAYMENT_GATEWAY_API_KEY=your_payment_gateway_api_key
PAYMENT_GATEWAY_SECRET=your_payment_gateway_secret
```

## Running the Application

```bash
# Development mode
npm run start:dev

# Production mode
npm run build
npm run start:prod

# Debug mode
npm run start:debug
```

## API Documentation

The API documentation is available through Swagger UI at `http://localhost:3000/api-docs` when the application is running.

### Main API Endpoints

#### Authentication
- POST `/auth/register` - Register a new user
  ```json
  {
    "email": "user@example.com",
    "password": "yourpassword",
    "firstName": "John",
    "lastName": "Doe",
    "role": "ADMIN"
  }
  ```
- POST `/auth/login` - User login
  ```json
  {
    "email": "user@example.com",
    "password": "yourpassword"
  }
  ```
- POST `/auth/generate-sign` - Generate sign for school and collect request
  ```json
  {
    "school_id": "school_id",
    "collect_request_id": "collect_request_id"
  }
  ```
- GET `/auth/profile` - Get user profile (Protected)

#### Payments
- POST `/create-payment` - Create a new payment and redirect to payment gateway (Protected)
  ```json
  {
    // Payment details as per CreatePaymentDto
  }
  ```
- GET `/payment-status/:collect_request_id` - Get payment status by collect request ID (Protected)
  - Query params: `school_id`

- POST `/webhook` - Webhook endpoint for payment status updates
  - Handles payment gateway callbacks
  - Updates transaction status

- GET `/transactions` - Get all transactions with pagination and filtering (Protected)
  - Query params:
    - `page` (default: 1)
    - `limit` (default: 10)
    - `sort` (default: 'payment_time')
    - `order` (default: 'desc')
    - `status` (optional)

- GET `/transactions/school/:schoolId` - Get school-specific transactions (Protected)
  - Query params:
    - `page` (default: 1)
    - `limit` (default: 10)
    - `sort` (default: 'payment_time')
    - `order` (default: 'desc')

- GET `/transaction-status/:customOrderId` - Check transaction status (Protected)

## Security Features

- JWT-based authentication
- Protected routes using Guards
- Password hashing using argon2
- Rate limiting for API endpoints
- Input validation and sanitization
- CORS protection
- Secure webhook handling

## Postman Collection

You can find the Postman collection for testing the API endpoints in the `postman` directory. To use it:

1. Open Postman
2. Click on "Import"
3. Select the `AcadPay.postman_collection.json` file
4. Set up environment variables:
   - `base_url`: Your API base URL (e.g., http://localhost:3000)
   - `token`: JWT token received after login
   - Other variables as needed for testing

## Testing

```bash
# Unit tests
npm run test

# e2e tests
npm run test:e2e

# Test coverage
npm run test:cov
```

## Error Handling

The API uses standard HTTP response codes:
- 200: Success
- 201: Created
- 400: Bad Request
- 401: Unauthorized
- 403: Forbidden
- 404: Not Found
- 500: Internal Server Error

## Contributing

1. Fork the repository
2. Create your feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit your changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to the branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## License

This project is licensed under the MIT License - see the LICENSE file for details.

## Support

For support, please email abhishekhede4@gmail.com or open an issue in the GitHub repository.

---

Built with [NestJS](https://nestjs.com/) 🚀
