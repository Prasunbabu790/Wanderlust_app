# 🌍 Wanderlust — Vacation Rentals & Experiences Marketplace

A feature-rich, full-stack travel and hospitality web application inspired by Airbnb, designed to connect travelers with unique accommodations and unforgettable local experiences around the globe.

🚀 **Live Deployment:** [https://wanderlust-app-n1f4.onrender.com/listings](https://wanderlust-app-n1f4.onrender.com/listings)

---

## 📖 Project Description

**Wanderlust** is a modern online marketplace for vacation rentals, villas, cabins, and unique stays. Built on the **Node.js**, **Express.js**, and **MongoDB** ecosystem, the platform allows users to explore accommodations across various categories, view interactive geo-located maps, submit verified customer reviews with star ratings, and list their own properties.

The application adheres to the **MVC (Model-View-Controller)** architectural pattern and features robust authentication, role-based authorization, cloud-based media storage, and real-time forward geocoding.

---

## ✨ Features

### 🏡 Listing Management (CRUD)
* **Explore Stays:** Browse vacation rentals with high-resolution imagery, pricing, and locations.
* **Add Listings:** Authenticated users can create new listings with cloud image uploads.
* **Edit & Update:** Hosts can edit their own property descriptions, pricing, locations, and images.
* **Delete Listings:** Hosts can delete listings; associated reviews are automatically cleaned up using Mongoose cascade deletion middleware.

### 🗺️ Interactive Geolocation & Maps
* **Mapbox Integration:** Forward geocoding converts address and location text into geographic coordinates.
* **Interactive Map View:** Visualizes listing locations on interactive Mapbox maps with custom markers and popup previews.

### ⭐ Ratings & Reviews System
* **Leave Reviews:** Authenticated travelers can share feedback and rating scores (1 to 5 stars) using an animated star rating interface.
* **Delete Reviews:** Review authors have permissions to delete their own reviews.

### 🏷️ Category Filtering & Dynamic Tax Toggle
* **Category Filters:** Quick filter icons for Trending, Rooms, Iconic Cities, Mountains, Castles, Pools, Camping, Farms, Arctic, Domes, and Boats.
* **GST Tax Calculator:** One-click toggle switch to dynamically calculate and display prices inclusive of 18% GST.

### 🔐 Authentication & Authorization
* **User Accounts:** Secure registration, login, and logout powered by Passport.js (`passport-local`).
* **Session Persistence:** Persistent login sessions stored in MongoDB Atlas via `connect-mongo`.
* **Access Control:** Middleware guards ensure only listing owners can modify listings and only review authors can delete their reviews.

### 🛡️ Validation & Error Handling
* **Schema Validation:** Comprehensive server-side schema validation using **Joi**.
* **Client-side Validation:** Responsive Bootstrap 5 validation states.
* **Custom Error Handling:** Unified `ExpressError` handler and asynchronous wrapper utility (`wrapAsync`).

### ☁️ Cloud Asset Management
* **Cloudinary & Multer:** Direct and secure cloud-hosted image upload pipeline with automatic image optimization.

---

## 🛠️ Technologies Used

### Frontend
* **EJS & EJS-Mate:** Dynamic server-side templating and layout boilerplate engine
* **HTML5 & CSS3:** Semantic markup and custom modern stylesheets
* **Bootstrap 5:** Responsive UI components and grid system
* **Font Awesome:** Vector icons for categories and UI actions
* **Starability CSS:** Accessible, pure CSS star rating widgets
* **Mapbox GL JS:** Interactive, client-side vector maps

### Backend & Database
* **Node.js:** Server-side JavaScript runtime environment
* **Express.js:** Fast, minimalist web framework (MVC architecture)
* **MongoDB & MongoDB Atlas:** NoSQL document database & cloud cluster
* **Mongoose ODM:** Data modeling with schema definitions, pre/post hooks, and relationships

### Authentication & Cloud Services
* **Passport.js & Passport-Local:** Authentication middleware with salt & hashing algorithms
* **Express-Session & Connect-Mongo:** Stateful cookie sessions backed by MongoStore
* **Connect-Flash:** Transient flash messages for feedback and alerts
* **Cloudinary & Multer-Storage-Cloudinary:** Cloud storage and image processing
* **Mapbox Geocoding SDK:** Real-time forward address-to-coordinate geocoding

### Validation & Utilities
* **Joi:** Schema description language and data validator
* **Method-Override:** Enables RESTful `PUT` and `DELETE` HTTP verbs from HTML forms
* **Dotenv:** Secure environment variable management

---

## 📂 Project Structure

```text
Wanderlust_app/
│
├── controllers/              # Application business logic (MVC Controllers)
│   ├── listings.js           # Listing CRUD and geocoding logic
│   ├── reviews.js            # Review creation and deletion logic
│   └── users.js              # Authentication and session logic
│
├── init/                     # Database seeding and mock data
│   ├── data.js               # Sample listing dataset
│   └── index.js              # Database initialization script
│
├── models/                   # Mongoose schemas and models
│   ├── listing.js            # Listing model with geometry & review references
│   ├── review.js             # Review model with rating & author
│   └── user.js               # User model with passport-local-mongoose
│
├── public/                   # Static client-side assets
│   ├── css/
│   │   ├── rating.css        # Starability star rating styling
│   │   └── style.css         # Global design system and custom UI styles
│   └── js/
│       ├── map.js            # Mapbox initialization & marker rendering
│       └── script.js         # Bootstrap form validation script
│
├── routes/                   # Express route handlers
│   ├── listing.js            # /listings routes
│   ├── review.js             # /listings/:id/reviews routes
│   └── user.js               # /signup, /login, /logout routes
│
├── utils/                    # Helper functions and error utilities
│   ├── ExpressError.js       # Custom error class
│   └── wrapAsync.js          # Async error catching wrapper
│
├── views/                    # EJS views and templates
│   ├── includes/             # Partials (navbar, footer, flash alerts)
│   │   ├── flash.ejs
│   │   ├── footer.ejs
│   │   └── navbar.ejs
│   ├── layouts/              # Master layout wrapper
│   │   └── boilerplate.ejs
│   ├── listings/             # Listing views (index, show, new, edit, error)
│   │   ├── edit.ejs
│   │   ├── error.ejs
│   │   ├── index.ejs
│   │   ├── new.ejs
│   │   └── show.ejs
│   └── users/                # Authentication views
│       ├── login.ejs
│       └── signup.ejs
│
├── .env.example              # Sample environment variables template
├── .gitignore                # Git ignored files (node_modules, .env)
├── app.js                    # Express application entry point & middleware setup
├── cloudConfig.js            # Cloudinary & Multer configuration
├── middlewere.js             # Auth, owner, and Joi validation middlewares
├── package.json              # Project dependencies and metadata
└── schema.js                 # Joi validation schemas
```

---

## 🚦 RESTful API Routes

| Endpoint | Method | Description | Authentication / Authorization |
| :--- | :--- | :--- | :--- |
| `/listings` | `GET` | Display all listings with category filters | Public |
| `/listings/new` | `GET` | Render form to create a new listing | Logged-in User |
| `/listings` | `POST` | Create new listing with image upload & geocoding | Logged-in User |
| `/listings/:id` | `GET` | View details of a specific listing with Map & Reviews | Public |
| `/listings/:id/edit` | `GET` | Render edit form for listing | Listing Owner |
| `/listings/:id` | `PUT` | Update listing details & optional new image | Listing Owner |
| `/listings/:id` | `DELETE` | Delete listing and cascade delete its reviews | Listing Owner |
| `/listings/:id/reviews` | `POST` | Add a rating and comment to a listing | Logged-in User |
| `/listings/:id/reviews/:reviewId` | `DELETE` | Delete a specific review | Review Author |
| `/signup` | `GET` / `POST` | Render signup form / Register new user | Public |
| `/login` | `GET` / `POST` | Render login form / Authenticate user | Public |
| `/logout` | `GET` | End user session & clear cookies | Logged-in User |

---

## 🚀 Getting Started

### Prerequisites

Ensure you have the following installed on your machine:
* [Node.js](https://nodejs.org/) (v18 or higher recommended)
* [MongoDB](https://www.mongodb.com/) (Local instance or MongoDB Atlas cluster)
* A free account on [Cloudinary](https://cloudinary.com/) (for cloud image storage)
* A free account on [Mapbox](https://www.mapbox.com/) (for geolocation & maps)

---

### Installation & Setup

1. **Clone the Repository**
   ```bash
   git clone https://github.com/Prasunbabu790/Wanderlust_app.git
   cd Wanderlust_app
   ```

2. **Install Dependencies**
   ```bash
   npm install
   ```

3. **Configure Environment Variables**
   
   Create a `.env` file in the root directory and add the following keys:
   ```env
   # Database & Session Configuration
   ATLASDB_URL=mongodb+srv://<username>:<password>@cluster0.mongodb.net/wanderlust?retryWrites=true&w=majority
   SECRET=your_super_secret_session_key
   
   # Cloudinary Media Storage Credentials
   CLOUD_NAME=your_cloudinary_cloud_name
   CLOUD_API_KEY=your_cloudinary_api_key
   CLOUD_API_SECRET=your_cloudinary_api_secret
   
   # Mapbox API Token
   MAP_TOKEN=your_mapbox_public_access_token
   ```

4. **Initialize / Seed Sample Data (Optional)**
   ```bash
   node init/index.js
   ```

5. **Start the Application**
   ```bash
   node app.js
   ```
   *or with nodemon for live reload:*
   ```bash
   npx nodemon app.js
   ```

6. **Access in Browser**
   
   Open your browser and navigate to:
   ```
   http://localhost:8080/listings
   ```

---

## 📸 Screenshots

| Browse Listings & Categories | Listing Details & Interactive Map |
| :---: | :---: |
| ![Explore Listings](https://images.unsplash.com/photo-1501785888041-af3ef285b470?auto=format&fit=crop&w=800&q=80) | ![Listing Details & Map](https://images.unsplash.com/photo-1566073771259-6a8506099945?auto=format&fit=crop&w=800&q=80) |

| User Reviews & Star Ratings | Add & Edit Property Listings |
| :---: | :---: |
| ![Reviews & Ratings](https://images.unsplash.com/photo-1582719508461-905c673771fd?auto=format&fit=crop&w=800&q=80) | ![Add New Stay](https://images.unsplash.com/photo-1512917774080-9991f1c4c750?auto=format&fit=crop&w=800&q=80) |

---

## 🔮 Future Enhancements

* 💳 **Payment Gateway Integration:** Secure online booking & payment checkout using Stripe or Razorpay.
* 📅 **Reservation Calendar:** Date picker with real-time room availability and booking management.
* 🔍 **Advanced Search & Filters:** Search by destination city, price range sliders, guest count, and specific amenities.
* 👤 **Host & User Dashboard:** User profile pages showing booking history, active listings, and earnings metrics.
* 💬 **Real-time Messaging:** Direct chat between hosts and guests using WebSockets / Socket.io.
* 🌙 **Dark Mode & Multi-Currency:** Theme switcher and real-time currency conversion rates.

---

## 🎓 Learning Outcomes

Through building Wanderlust, key full-stack concepts mastered include:

* **MVC Pattern & Clean Code:** Structuring scalable backend applications separating models, views, controllers, and routes.
* **Relational Schema Design in NoSQL:** Managing 1:Many relationships, Object ID references, and Mongoose cascade delete hooks.
* **Authentication & Security:** Implementing session-based authentication, password hashing, salt generation, and route guards with Passport.js.
* **Third-Party API Integrations:** Working with Mapbox SDK for forward geocoding and rendering vector maps on the frontend.
* **Cloud Storage & Multipart Uploads:** Handling multipart form data with Multer and streaming media to Cloudinary.
* **Data Validation & Resiliency:** Implementing dual-layer validation (Joi on server, Bootstrap on client) and error handling middleware.

---

## 👨‍💻 Author

**Prasun Babu**

* **Live Demo:** [wanderlust-app-n1f4.onrender.com/listings](https://wanderlust-app-n1f4.onrender.com/listings)
* **GitHub:** [@Prasunbabu790](https://github.com/Prasunbabu790)
* **Project Repository:** [Wanderlust_app](https://github.com/Prasunbabu790/Wanderlust_app)

---

## ⭐ Support

If you found this project helpful or inspiring, please consider giving it a **Star** ⭐ on GitHub!

Thank you for exploring Wanderlust! 🚀
