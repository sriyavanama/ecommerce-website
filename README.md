# sriyavanama Store - E-Commerce Application

A full-stack e-commerce application built with Spring Boot backend and React frontend, featuring WhatsApp integration for order notifications and Razorpay payment gateway integration.

## Table of Contents

- [Project Overview](#project-overview)
- [Features](#features)
- [Technology Stack](#technology-stack)
- [Project Structure](#project-structure)
- [Prerequisites](#prerequisites)
- [Installation & Setup](#installation--setup)
  - [Backend Setup](#backend-setup)
  - [Frontend Setup](#frontend-setup)
- [Environment Configuration](#environment-configuration)
- [API Endpoints](#api-endpoints)
- [Database Schema](#database-schema)
- [Usage](#usage)
- [Screenshots](#screenshots)
- [Contributing](#contributing)

## Project Overview

sriyavanama Store is a modern e-commerce platform that allows customers to:
- Browse products across categories (Laptops, Mobiles, Headphones)
- Add items to cart with quantity selection
- Secure user authentication
- Complete purchases using Razorpay payment gateway
- Receive order confirmations via WhatsApp

## Features

### Core E-Commerce Features
- **Product Catalog**: Browse laptops, mobiles, and headphones
- **Shopping Cart**: Add, remove, and manage cart items
- **User Authentication**: Secure login system
- **Payment Integration**: Razorpay payment gateway
- **Order Summary**: Detailed invoice generation

### Communication Features
- **WhatsApp Integration**: Order confirmations sent via Twilio WhatsApp API
- **Real-time Cart Updates**: Dynamic cart count and total calculation

### UI/UX Features
- **Responsive Design**: Mobile-friendly interface
- **Modern Icons**: React Icons integration
- **Smooth Navigation**: React Router for seamless page transitions

## Technology Stack

### Backend (ecomm-backend)
- **Framework**: Spring Boot 3.5.3
- **Language**: Java 17
- **Database**: MySQL 8.0+
- **ORM**: Spring Data JPA with Hibernate
- **Build Tool**: Maven
- **Libraries**:
  - Lombok (Boilerplate code reduction)
  - Twilio SDK (WhatsApp integration)
  - Spring Boot DevTools (Development)

### Frontend (ecomme-frontend)
- **Framework**: React 19.1.0
- **Build Tool**: Vite 7.0.4
- **Language**: JavaScript (ES6+)
- **Routing**: React Router DOM 6.30.1
- **HTTP Client**: Axios 1.10.0
- **UI Icons**: React Icons 5.5.0
- **Styling**: CSS3

## Project Structure

```
ecommerce-project-master/
├── ecomm-backend/                 # Spring Boot Backend
│   ├── src/main/java/com/excelr/
│   │   ├── config/
│   │   │   └── TwilioConfig.java          # Twilio configuration
│   │   ├── controller/
│   │   │   └── ExcelRController.java      # REST API endpoints
│   │   ├── model/
│   │   │   ├── Laptops.java               # Laptop entity
│   │   │   ├── Mobiles.java               # Mobile entity
│   │   │   ├── Headphones.java            # Headphone entity
│   │   │   ├── Login.java                 # User entity
│   │   │   └── WhatsAppRequest.java       # WhatsApp request DTO
│   │   ├── repo/
│   │   │   ├── LaptopsRepo.java           # Laptop repository
│   │   │   ├── MobilesRepo.java           # Mobile repository
│   │   │   ├── HeadPhonesRepo.java        # Headphone repository
│   │   │   └── LoginRepo.java             # User repository
│   │   ├── service/
│   │   │   └── ExcelRService.java         # Business logic
│   │   └── EcommBackendApplication.java   # Main application class
│   ├── src/main/resources/
│   │   └── application.properties         # Configuration file
│   └── pom.xml                           # Maven dependencies
│
├── ecomme-frontend/              # React Frontend
│   ├── src/
│   │   ├── components/
│   │   │   ├── Dashboard.jsx             # Main dashboard component
│   │   │   ├── Login.jsx                 # Authentication component
│   │   │   ├── Laptops.jsx               # Laptop listing component
│   │   │   ├── Mobiles.jsx               # Mobile listing component
│   │   │   ├── Headphones.jsx            # Headphone listing component
│   │   │   ├── CartSummary.jsx           # Cart & payment component
│   │   │   ├── CartContext.jsx           # Cart state management
│   │   │   ├── DetailedProduct.jsx       # Product details view
│   │   │   ├── Master.jsx                # Route configuration
│   │   │   ├── ThankYou.jsx              # Order confirmation
│   │   │   └── *.css                     # Component styles
│   │   ├── App.jsx                       # Root component
│   │   ├── main.jsx                      # Application entry point
│   │   └── index.css                     # Global styles
│   ├── package.json                      # NPM dependencies
│   └── vite.config.js                   # Vite configuration
│
└── README.md                            # This file
```

## Prerequisites

Before setting up the project, ensure you have:

### Software Requirements
- **Java**: JDK 17 or higher
- **Node.js**: Version 18 or higher
- **npm**: Version 9 or higher
- **MySQL**: Version 8.0 or higher
- **Maven**: Version 3.6 or higher

### Third-party Accounts
- **Twilio Account**: For WhatsApp messaging
- **Razorpay Account**: For payment processing

## Installation & Setup

### Backend Setup

1. **Navigate to backend directory**
   ```bash
   cd ecomm-backend
   ```

2. **Set up MySQL Database**
   ```sql
   CREATE DATABASE ecommerce_db;
   ```

3. **Configure Environment Variables**
   Create a `.env` file or set system environment variables:
   ```bash
   DB_URL=jdbc:mysql://localhost:3306/ecommerce_db
   DB_USER=your_mysql_username
   DB_PASS=your_mysql_password
   TWILIO_ACCOUNT_SID=your_twilio_account_sid
   TWILIO_AUTH_TOKEN=your_twilio_auth_token
   TWILIO_WHATSAPP_NUMBER=whatsapp:+your_twilio_number
   TWILIO_CERTIFIED_NUMBER=+recipient_phone_number
   RAZORPAY_KEY_SECRET=your_razorpay_key
   ```

4. **Install Dependencies & Run**
   ```bash
   # Using Maven
   ./mvnw spring-boot:run
   
   # Or using Maven directly
   mvn spring-boot:run
   ```

   The backend server will start on `http://localhost:5001`

### Frontend Setup

1. **Navigate to frontend directory**
   ```bash
   cd ecomme-frontend
   ```

2. **Install Dependencies**
   ```bash
   npm install
   ```

3. **Start Development Server**
   ```bash
   npm run dev
   ```

   The frontend will start on `http://localhost:5173`

## Environment Configuration

### Backend Configuration (`application.properties`)
```properties
# Application
spring.application.name=ecomm-backend
server.port=5001

# Database
spring.datasource.url=${DB_URL}
spring.datasource.username=${DB_USER}
spring.datasource.password=${DB_PASS}
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver

# JPA/Hibernate
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.MySQLDialect

# Twilio WhatsApp
twilio.account.sid=${TWILIO_ACCOUNT_SID}
twilio.auth.token=${TWILIO_AUTH_TOKEN}
twilio.from.whatsapp=${TWILIO_WHATSAPP_NUMBER}
twilio.certified.number=${TWILIO_CERTIFIED_NUMBER}

# Razorpay
razorpay.key.secret=${RAZORPAY_KEY_SECRET}
```

### Frontend Configuration
Update API endpoints in components if needed:
- Default backend URL: `http://localhost:5001`
- Razorpay test key: `rzp_test_1DP5mmOlF5G5ag`

## API Endpoints

### Product Endpoints
```http
GET /laptops          # Get all laptops
GET /mobiles          # Get all mobiles
GET /headphones       # Get all headphones
```

### Authentication
```http
POST /login           # User authentication
Content-Type: application/json
{
  "username": "string",
  "password": "string"
}
```

### WhatsApp Integration
```http
POST /send-whatsapp   # Send WhatsApp message
Content-Type: application/json
{
  "message": "string"
}
```

## Database Schema

### Products Tables
```sql
-- Laptops
CREATE TABLE laptops (
    pid INT PRIMARY KEY AUTO_INCREMENT,
    pname VARCHAR(255),
    pcost DOUBLE,
    pqty INT,
    pimage VARCHAR(255)
);

-- Mobiles
CREATE TABLE mobiles (
    pid INT PRIMARY KEY AUTO_INCREMENT,
    pname VARCHAR(255),
    pcost DOUBLE,
    pqty INT,
    pimage VARCHAR(255)
);

-- Headphones
CREATE TABLE headphones (
    pid INT PRIMARY KEY AUTO_INCREMENT,
    pname VARCHAR(255),
    pcost DOUBLE,
    pqty INT,
    pimage VARCHAR(255)
);

-- Users
CREATE TABLE login (
    id INT PRIMARY KEY AUTO_INCREMENT,
    username VARCHAR(255) UNIQUE,
    password VARCHAR(255)
);
```

## Usage

### For Customers:
1. **Login**: Use credentials to access the store
2. **Browse**: Navigate through product categories
3. **Shop**: Add items to cart with desired quantities
4. **Checkout**: Review cart and proceed to payment
5. **Pay**: Complete purchase using Razorpay
6. **Confirm**: Receive WhatsApp confirmation

### For Developers:
1. **Add Products**: Insert data directly into MySQL tables
2. **Customize UI**: Modify React components and CSS
3. **Configure Payment**: Update Razorpay keys
4. **Setup WhatsApp**: Configure Twilio credentials

## Development Commands

### Backend
```bash
# Build project
./mvnw clean compile

# Run tests
./mvnw test

# Package application
./mvnw clean package

# Run with different profile
./mvnw spring-boot:run -Dspring.profiles.active=dev
```

### Frontend
```bash
# Development server
npm run dev

# Build for production
npm run build

# Preview production build
npm run preview

# Lint code
npm run lint
```

## Troubleshooting

### Common Issues

1. **PowerShell Execution Policy Error**
   ```powershell
   Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
   ```

2. **Database Connection Issues**
   - Verify MySQL is running
   - Check database credentials
   - Ensure database exists

3. **Twilio WhatsApp Issues**
   - Verify sandbox setup in Twilio console
   - Check phone number format (+country_code)
   - Ensure WhatsApp number is verified

4. **Payment Integration Issues**
   - Verify Razorpay test keys
   - Check network connectivity
   - Ensure HTTPS for production

## Screenshots

### Login Page
- Clean authentication interface
- Error handling for invalid credentials

### Dashboard
- Category-wise product navigation
- Real-time cart counter
- Welcome screen with store branding

### Product Listings
- Grid layout for products
- Product details with pricing
- Add to cart functionality

### Cart Summary
- Invoice-style layout
- Quantity management
- Total calculation
- Payment integration

### Order Confirmation
- Thank you page
- WhatsApp notification status

## Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/AmazingFeature`)
3. Commit changes (`git commit -m 'Add some AmazingFeature'`)
4. Push to branch (`git push origin feature/AmazingFeature`)
5. Open a Pull Request

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Support

For support and queries:
- Email: support@sriyavanama.com
- Phone: +91-9999999999
- WhatsApp: Available through the application

## Acknowledgments

- Spring Boot community for excellent documentation
- React team for the amazing framework
- Twilio for WhatsApp integration
- Razorpay for payment processing
- All contributors and testers

---

**Built with love by the sriyavanama Store Team**

*Happy Shopping!*
