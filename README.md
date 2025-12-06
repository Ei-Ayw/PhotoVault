# Photo Gallery - Laravel 11 Application

A minimalist personal photo gallery system built with Laravel 11, featuring user authentication, role-based authorization, image watermarking, and a beautiful responsive UI.

## 🎓 University Assignment

This is a high-grade course assignment demonstrating:
- **MVC Architecture** with clear separation of concerns
- **Advanced Image Processing** with automatic watermarking
- **Policy-based Authorization** for role management
- **Responsive UI/UX** with Tailwind CSS
- **Cross-platform Compatibility** (Windows & AWS Ubuntu)

## 🚀 Features

### Core Functionality
- ✅ **User Authentication** (Laravel Breeze)
- ✅ **Photo Upload** with automatic watermarking
- ✅ **Role-based Access Control** (Regular Users & Administrators)
- ✅ **Responsive Grid Layout** (Tailwind CSS)
- ✅ **Image Validation** (JPG, PNG, max 2MB)
- ✅ **Pagination** (12 photos per page)

### Authorization Rules (PhotoPolicy)
- **View**: Public access (guests & authenticated users)
- **Create**: Authenticated users only
- **Delete**: 
  - Regular users can delete their own photos
  - Administrators can delete ANY photo (content moderation)

### Advanced Features
- 🎨 **Automatic Watermarking**: Uploader's username added to bottom-right corner
- 📱 **Fully Responsive**: Grid layout adapts to all screen sizes
- 🔒 **Secure File Upload**: Validation and sanitization
- ⚡ **Performance**: Optimized with eager loading and pagination

## 📋 Technical Stack

- **Framework**: Laravel 11
- **Frontend**: Blade Templates + Tailwind CSS
- **Authentication**: Laravel Breeze (Blade version)
- **Database**: MySQL
- **Image Processing**: Intervention Image 3.x
- **PHP Version**: 8.2+ (tested with 8.3.26)

## 🔧 Installation Instructions

### Prerequisites
- PHP 8.2 or higher
- Composer
- MySQL
- Node.js & NPM

### Setup Steps

#### 1. Install Dependencies
```bash
cd photo-gallery
composer install
npm install
```

#### 2. Environment Configuration
The `.env` file is already configured for local MySQL:
- Database: `photo_gallery`
- Host: `localhost` (127.0.0.1)
- Port: `3306`
- Username: `root`
- Password: `123456`

If your MySQL credentials are different, update the `.env` file accordingly.

#### 3. Create Database
Start your MySQL server, then create the database:
```bash
mysql -u root -p
CREATE DATABASE photo_gallery CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
exit;
```

Or use the command:
```bash
mysql -u root -p123456 -e "CREATE DATABASE photo_gallery CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;"
```

#### 4. Run Migrations
```bash
php artisan migrate
```

This will create:
- `users` table with `is_admin` column
- `photos` table with all required fields
- Other Laravel default tables

#### 5. Create Storage Link
```bash
php artisan storage:link
```

This creates a symbolic link from `public/storage` to `storage/app/public` for serving uploaded photos.

#### 6. Build Frontend Assets
```bash
npm run build
```

For development:
```bash
npm run dev
```

#### 7. Start Development Server
```bash
php artisan serve
```

Visit: `http://localhost:8000`

## 👤 Creating Admin Users

To create an administrator account:

1. Register a normal user through the web interface
2. Manually update the database:
```sql
UPDATE users SET is_admin = 1 WHERE email = 'admin@example.com';
```

Or use Laravel Tinker:
```bash
php artisan tinker
>>> $user = User::where('email', 'admin@example.com')->first();
>>> $user->is_admin = true;
>>> $user->save();
```

## 📁 Project Structure

```
app/
├── Http/
│   ├── Controllers/
│   │   ├── Controller.php          # Base controller with AuthorizesRequests trait
│   │   └── PhotoController.php     # Complete CRUD with watermarking
│   └── ...
├── Models/
│   ├── User.php                     # User model with is_admin & photos relationship
│   └── Photo.php                    # Photo model with fillable & user relationship
├── Policies/
│   └── PhotoPolicy.php              # Authorization logic (viewAny, create, delete)
└── ...

database/
└── migrations/
    ├── *_add_is_admin_to_users_table.php
    └── *_create_photos_table.php

resources/
└── views/
    ├── photos/
    │   ├── index.blade.php          # Gallery homepage with grid
    │   ├── create.blade.php         # Upload form
    │   ├── show.blade.php           # Single photo view
    │   └── edit.blade.php           # Edit photo details
    └── layouts/
        ├── app.blade.php
        └── navigation.blade.php     # Updated with admin panel link

routes/
└── web.php                           # All routes defined
```

## 🎨 UI/UX Highlights

- **Modern Design**: Gradient backgrounds, smooth transitions, hover effects
- **Card-based Layout**: Clean photo cards with shadows and hover animations
- **Responsive Grid**: 1-4 columns based on screen size
- **Visual Feedback**: Success/error messages with animations
- **Conditional UI**: Action buttons shown based on user permissions (@can directive)
- **Loading States**: Lazy loading for images
- **Empty States**: Friendly messages when no photos exist

## 🔒 Security Features

- **CSRF Protection**: All forms protected
- **File Validation**: Type and size restrictions
- **Policy Authorization**: Explicit permission checks
- **SQL Injection Prevention**: Eloquent ORM
- **Mass Assignment Protection**: $fillable arrays
- **XSS Prevention**: Blade escaping

## 📝 Code Quality

All code includes:
- ✅ **English Comments**: Detailed explanations for assignment report
- ✅ **Clear Variable Names**: Self-documenting code
- ✅ **Proper Indentation**: PSR-12 coding standards
- ✅ **Error Handling**: Validation and user feedback
- ✅ **DRY Principle**: No code duplication

## 🌐 AWS Ubuntu Deployment

For production deployment on AWS Ubuntu:

1. Update `.env` file DATABASE settings:
```env
DB_CONNECTION=mysql
DB_HOST=your-rds-endpoint
DB_PORT=3306
DB_DATABASE=photo_gallery
DB_USERNAME=your-db-username
DB_PASSWORD=your-db-password
```

2. Set proper permissions:
```bash
chmod -R 775 storage bootstrap/cache
chown -R www-data:www-data storage bootstrap/cache
```

3. Configure Apache/Nginx to point to `public` directory

4. Run production build:
```bash
composer install --optimize-autoloader --no-dev
php artisan config:cache
php artisan route:cache
php artisan view:cache
npm run build
```

## 📚 Technologies Used

- **Laravel 11.x**: Latest PHP framework
- **Intervention Image 3.11**: Image manipulation with GD driver
- **Tailwind CSS**: Utility-first CSS framework
- **Alpine.js**: Lightweight JavaScript framework (via Breeze)
- **MySQL**: Relational database
- **Vite**: Frontend build tool

## 🎯 Assignment Requirements Met

- ✅ Laravel 11 & PHP 8.2+
- ✅ Blade Templates + Tailwind CSS
- ✅ Laravel Breeze Authentication
- ✅ MySQL Database with proper migrations
- ✅ Users table with `is_admin` field
- ✅ Photos table with all required columns
- ✅ PhotoPolicy with proper authorization
- ✅ PhotoController with CRUD operations
- ✅ Image watermarking (ADVANCED TECHNIQUE)
- ✅ Form validation (file type & size)
- ✅ Responsive grid layout
- ✅ Pagination (12 photos per page)
- ✅ @can directive for conditional UI
- ✅ Cross-platform file path handling
- ✅ English code comments

## 📄 License

This is a university assignment project. For educational purposes only.

## 👨‍💻 Development Notes

- Watermarking uses Intervention Image with GD driver
- File paths use Laravel's `Storage` facade for cross-platform compatibility
- Authorization handled by Policy, not manual checks
- All routes follow RESTful conventions
- UI uses modern CSS3 animations and transitions

## 🐛 Troubleshooting

### MySQL Connection Error
```bash
# Start MySQL service
# Windows (XAMPP):
Start XAMPP and click "Start" for MySQL

# Windows (Standalone MySQL):
net start MySQL80

# Ubuntu:
sudo service mysql start
```

### Storage Link Not Working
```bash
# Remove existing link and recreate
rm public/storage
php artisan storage:link
```

### Images Not Displaying
Check that:
1. Storage link exists: `public/storage` → `storage/app/public`
2. Folder permissions are correct (775)
3. Images are in `storage/app/public/photos/`

## 📞 Support

For questions about this assignment, please refer to the inline code comments or contact the course instructor.

---

**Built with ❤️ for COMP10015 Course Assignment**
