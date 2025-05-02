
# **ClickToCodeBot**

**Telegram Bot** for developers to accept orders, submit questions, and communicate with admins. This bot provides a smooth interface for developers and admins to interact seamlessly.

## **Project Structure**

### **1. Project Setup**

Follow these steps to set up the project on your local machine:

#### **Step 1: Clone the Repository**
Clone this repository to your local machine:
```bash
[git clone https://github.com/your-username/ClickToCodeBot.git](https://github.com/AbdualimovBotir/ClickToCodeBot.git)
```

#### **Step 2: Open the Project in Your IDE**
Open the project in **IntelliJ IDEA** or **Eclipse**.

#### **Step 3: Build the Project**
Use Maven or Gradle to build the project:
```bash
mvn clean install
```

#### **Step 4: Set up the Database**
Create a PostgreSQL database and apply the schema from the provided SQL files.

```sql
-- Database Schema

CREATE TABLE users (
  id SERIAL PRIMARY KEY,
  telegram_id BIGINT UNIQUE NOT NULL,
  full_name VARCHAR(100),
  phone_number VARCHAR(20),
  is_verified BOOLEAN DEFAULT false,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE questions (
  id SERIAL PRIMARY KEY,
  user_id INTEGER REFERENCES users(id),
  message TEXT,
  is_answered BOOLEAN DEFAULT false,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE orders (
  id SERIAL PRIMARY KEY,
  user_id INTEGER REFERENCES users(id),
  service_type VARCHAR(100),
  description TEXT,
  budget INTEGER,
  status VARCHAR(20) DEFAULT 'pending',
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE admins (
  id SERIAL PRIMARY KEY,
  telegram_id BIGINT UNIQUE NOT NULL,
  username VARCHAR(50) UNIQUE,
  password TEXT NOT NULL,
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE replies (
  id SERIAL PRIMARY KEY,
  admin_id INTEGER REFERENCES admins(id),
  question_id INTEGER REFERENCES questions(id),
  order_id INTEGER REFERENCES orders(id),
  message TEXT,
  sent_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

### **2. Application Properties**
Configure the database connection and other essential settings in `src/main/resources/application.properties`:

```properties
spring.application.name=ClickToCodeBot
# Server port
server.port=8080

# Spring datasource configuration
spring.datasource.url=jdbc:postgresql://localhost:5432/your_database
spring.datasource.username=your_username
spring.datasource.password=your_password
spring.datasource.driver-class-name=org.postgresql.Driver
#spring.datasource.initialization-mode=always
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
spring.jpa.properties.hibernate.format_sql=true
spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.PostgreSQLDialect

# Telegram Bot Configuration
telegram.bot.token=your_bot_token
telegram.bot.username=your_bot_username

# Logging
logging.level.org.springframework.web=INFO
logging.level.com.yourcompany=DEBUG

# Admin credentials (optional, can be changed to secure authentication method)
#admin.username=admin
#admin.password=your_admin_password

# Security settings (optional, if you have JWT or session-based authentication)
#spring.security.user.name=admin
#spring.security.user.password=admin_password

# Time zone and Locale settings for Uzbekistan
spring.jackson.time-zone=Asia/Tashkent
spring.jackson.locale=uz_UZ

```

### **3. Running the Application**
Run the application using Spring Boot:

```bash
mvn spring-boot:run
```

Your **ClickToCodeBot** will be running at `http://localhost:8080`.


---

## **Database Diagram**

Below is the **DB Diagram** for the ClickToCodeBot project, outlining the tables and relationships.

```plaintext
Table users {
  id integer [primary key, increment]
  telegram_id bigint [unique, not null]
  full_name varchar(100)
  phone_number varchar(20)
  is_verified boolean [default: false]
  created_at timestamp [default: CURRENT_TIMESTAMP]
}

Table questions {
  id integer [primary key, increment]
  user_id integer [ref: > users.id]
  message text
  is_answered boolean [default: false]
  created_at timestamp [default: CURRENT_TIMESTAMP]
}

Table orders {
  id integer [primary key, increment]
  user_id integer [ref: > users.id]
  service_type varchar(100)
  description text
  budget integer
  status varchar(20) [default: 'pending']
  created_at timestamp [default: CURRENT_TIMESTAMP]
}

Table admins {
  id integer [primary key, increment]
  telegram_id bigint [unique, not null]
  username varchar(50) [unique]
  password text [not null]
  created_at timestamp [default: CURRENT_TIMESTAMP]
}

Table replies {
  id integer [primary key, increment]
  admin_id integer [ref: > admins.id]
  question_id integer [ref: > questions.id, null]
  order_id integer [ref: > orders.id, null]
  message text
  sent_at timestamp [default: CURRENT_TIMESTAMP]
}
```


---

## **Bot Features**

### **1. User Registration**
- Users can register by providing their Telegram ID, full name, and phone number.
- Verification status will be initially set to `false`.

### **2. Submit Questions**
- Users can submit questions to the bot, which will be stored in the `questions` table.
- The admin can respond to these questions through the bot interface.

### **3. Order Submission**
- Developers can submit orders for paid services through the bot.
- The orders will be stored in the `orders` table with details like service type, description, and budget.

### **4. Admin Dashboard**
- Admins can manage the submitted questions and orders.
- Admins can reply to users' questions and orders, with replies being stored in the `replies` table.

### **5. Notifications**
- Users will receive notifications for order status updates and replies to their questions.

---

## **Technologies Used**
- **Spring Boot**: For backend services.
- **PostgreSQL**: For database management.
- **Java**: Core programming language.
- **Telegram API**: For bot interactions.
- **JPA/Hibernate**: For ORM and database handling.
- **Maven**: For dependency management and build.

---

## **Contributing**
If you want to contribute to this project, feel free to fork this repository, submit issues, or open pull requests. Contributions are always welcome!

---

## **Contact**
For any inquiries, feel free to contact me:

- **Telegram**: [@botir_d3v](https://t.me/botir_d3v)
- **GitHub**: [git clone https://github.com/your-username/ClickToCodeBot.git](https://github.com/AbdualimovBotir/ClickToCodeBot.git)
- **Telegram_Chanel**: [@botir\_fullstack\_dev](https://t.me/botir_fullstack_dev)
- **LinkedIn**: [Botir Abdualimov](https://www.linkedin.com/in/botir-abdualimov-355060259)
- **Instagram**: [@botir\_d3v](https://www.instagram.com/botir_d3v?igsh=YmE4Nmg4ZmZ1ZWMy&utm_source=qr)
