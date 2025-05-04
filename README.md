# Airbnb Clone Project

## About the Project
The **Airbnb Clone Project** aims to develop a fullstack application that simulates the core functionality of Airbnb. This application will connect property owners with potential renters, providing a platform for short-term accommodation listings, bookings, and payments. The project will deliver a user-friendly interface with essential features found in the original Airbnb platform.

## Problem Statement
The short-term rental market continues to grow globally, creating opportunities for property monetization and convenient travel accommodations. This project addresses the need for a scalable, reliable web platform that facilitates these connections and transactions, simulating the successful Airbnb business model in a learning/development context

## Team roles

1. **Project Manager** - Oversees the entire project lifecycle, coordinates team activities, manages timeline and deliverables, communicates with stakeholders, and ensures project goals are met.

2. **Product Owner** - Defines product vision, prioritizes features, manages backlog, ensures alignment with business goals, and makes key product decisions.

3. **UX/UI Designer** - Creates user-centered interface designs, develops wireframes and prototypes, designs visual elements, and ensures intuitive user experience across the application.

4. **iOS Developer** - Builds and maintains the iOS version of the application using Swift, implements UI designs, integrates APIs, and ensures performance optimization for Apple devices.

5. **Android Developer** - Develops the Android version of the application using Kotlin or Java, implements UI components, integrates backend services, and optimizes for various Android devices.

6. **Backend Developer** - Creates and maintains server-side architecture, develops APIs, handles database management, implements business logic, and ensures secure data processing.

7. **DevOps Engineer** - Manages deployment infrastructure, sets up CI/CD pipelines, monitors application performance, handles scalability, and maintains development environments.

8. **QA Specialist** - Develops and executes test plans, performs manual and automated testing, identifies bugs, verifies fixes, and ensures overall application quality.

9. **Database Administrator** - Designs database schema, optimizes queries, manages data integrity, handles backups, and ensures efficient data storage and retrieval.

10. **Frontend Team Lead** - Coordinates mobile development efforts, reviews code, resolves technical challenges, establishes coding standards, and mentors junior developers.

11. **Security Specialist** - Implements security protocols, conducts vulnerability assessments, ensures compliance with data protection regulations, and prevents security breaches.

12. **User Researcher** - Conducts user interviews and usability testing, gathers feedback, analyzes user behavior, and provides insights to improve product experience.

## Technology Stack
- **Backend Framework:** Django
- **Database:** MySQL
- **API:** GraphQL
- **Version Control:** GitHub
- **Deployment Tools:** Docker, GitHub Actions (for CI/CD)

## Database Design

## 1. Users
- **Fields:**
  - user_id (Primary Key)
  - email
  - password_hash
  - username
  - user_type (host, guest, or both)
- **Relationships:**
  - One user can have multiple properties (as a host)
  - One user can make multiple bookings (as a guest)
  - One user can write multiple reviews
  - One user can have multiple payments

## 2. Properties
- **Fields:**
  - property_id (Primary Key)
  - host_id (Foreign Key → Users)
  - title
  - description
  - price_per_night
  - location_id (Foreign Key → Locations)
- **Relationships:**
  - A property belongs to one user (host)
  - A property has one location
  - A property has one property category
  - A property can have multiple rooms
  - A property can have multiple property images
  - A property can have multiple amenities
  - A property can receive multiple bookings
  - A property can receive multiple reviews

## 3. Rooms
- **Fields:**
  - room_id (Primary Key)
  - property_id (Foreign Key → Properties)
  - room_type
  - capacity
  - description
- **Relationships:**
  - A room belongs to one property
  - A room can have multiple amenities

## 4. Property_Images
- **Fields:**
  - image_id (Primary Key)
  - property_id (Foreign Key → Properties)
  - image_url
  - caption
  - is_primary
- **Relationships:**
  - An image belongs to one property

## 5. Locations
- **Fields:**
  - location_id (Primary Key)
  - address
  - city
  - state/province
  - country
  - latitude
  - longitude
- **Relationships:**
  - A location can have multiple properties
  - A location can be used for geographic searches

## 6. Property_Category
- **Fields:**
  - category_id (Primary Key)
  - name
  - description
  - icon_url
- **Relationships:**
  - A category can be assigned to multiple properties

## 7. Amenities
- **Fields:**
  - amenity_id (Primary Key)
  - name
  - description
  - icon_url
- **Relationships:**
  - An amenity can be associated with multiple properties (many-to-many)
  - An amenity can be associated with multiple rooms (many-to-many)

## 8. Availability
- **Fields:**
  - availability_id (Primary Key)
  - property_id (Foreign Key → Properties)
  - date
  - is_available
  - price_modifier
- **Relationships:**
  - Availability records belong to one property
  - Availability affects which dates can be booked

## 9. Bookings
- **Fields:**
  - booking_id (Primary Key)
  - guest_id (Foreign Key → Users)
  - property_id (Foreign Key → Properties)
  - check_in_date
  - check_out_date
  - total_price
  - status (pending, confirmed, completed, canceled)
- **Relationships:**
  - A booking belongs to one user (guest)
  - A booking belongs to one property
  - A booking can have one payment
  - A booking can have one review

## 10. Payments
- **Fields:**
  - payment_id (Primary Key)
  - booking_id (Foreign Key → Bookings)
  - user_id (Foreign Key → Users)
  - amount
  - payment_date
  - payment_status
- **Relationships:**
  - A payment belongs to one booking
  - A payment belongs to one user

## 11. Reviews
- **Fields:**
  - review_id (Primary Key)
  - booking_id (Foreign Key → Bookings)
  - reviewer_id (Foreign Key → Users)
  - property_id (Foreign Key → Properties)
  - rating
  - comment
  - review_date
- **Relationships:**
  - A review belongs to one booking
  - A review belongs to one user (reviewer)
  - A review belongs to one property

## 12. Comments
- **Fields:**
  - comment_id (Primary Key)
  - review_id (Foreign Key → Reviews)
  - user_id (Foreign Key → Users)
  - comment_text
  - comment_date
- **Relationships:**
  - A comment belongs to one review
  - A comment belongs to one user

## Key Relationship Diagrams:

### User-centered relationships:
- User (1) → Properties (0..n)
- User (1) → Bookings (0..n)
- User (1) → Reviews (0..n)
- User (1) → Payments (0..n)
- User (1) → Comments (0..n)

### Property-centered relationships:
- Property (1) → User/Host (1)
- Property (1) → Location (1)
- Property (1) → Property_Category (1)
- Property (1) → Rooms (0..n)
- Property (1) → Property_Images (0..n)
- Property (1) → Availability (0..n)
- Property (1) → Bookings (0..n)
- Property (1) → Reviews (0..n)
- Property (n) ↔ Amenities (m) [Many-to-Many]

### Booking-centered relationships:
- Booking (1) → User/Guest (1)
- Booking (1) → Property (1)
- Booking (1) → Payment (0..1)
- Booking (1) → Review (0..1)
