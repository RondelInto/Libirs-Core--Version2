# Libris Core - Python Implementation Guide
## Step-by-Step Python/Django Conversion with Full Code Examples

---

## Quick Start Installation

```bash
# Create project directory
mkdir libris_core_python
cd libris_core_python

# Create virtual environment
python -m venv venv

# Activate virtual environment
# On Windows:
venv\Scripts\activate
# On macOS/Linux:
source venv/bin/activate

# Create requirements.txt
cat > requirements.txt << EOF
Django==4.2.7
djangorestframework==3.14.0
django-cors-headers==4.3.1
psycopg2-binary==2.9.9
pandas==2.1.3
numpy==1.26.2
matplotlib==3.8.2
seaborn==0.13.0
plotly==5.18.0
celery==5.3.4
redis==5.0.1
reportlab==4.0.7
openpyxl==3.1.2
Pillow==10.1.0
PyJWT==2.8.0
django-filter==23.5
gunicorn==21.2.0
python-dotenv==1.0.0
scipy==1.11.4
EOF

# Install dependencies
pip install -r requirements.txt

# Create Django project
django-admin startproject libris_core .

# Create Django apps
python manage.py startapp authentication
python manage.py startapp books
python manage.py startapp transactions
python manage.py startapp analytics
python manage.py startapp notifications
```

---

## Project Structure

```
libris_core_python/
├── manage.py
├── requirements.txt
├── .env
├── .gitignore
│
├── libris_core/
│   ├── __init__.py
│   ├── settings.py
│   ├── urls.py
│   ├── wsgi.py
│   └── asgi.py
│
├── authentication/
│   ├── __init__.py
│   ├── models.py
│   ├── views.py
│   ├── serializers.py
│   ├── urls.py
│   ├── admin.py
│   └── tests.py
│
├── books/
│   ├── __init__.py
│   ├── models.py
│   ├── views.py
│   ├── serializers.py
│   ├── urls.py
│   ├── admin.py
│   └── tests.py
│
├── transactions/
│   ├── __init__.py
│   ├── models.py
│   ├── views.py
│   ├── serializers.py
│   ├── urls.py
│   ├── admin.py
│   └── tests.py
│
├── analytics/
│   ├── __init__.py
│   ├── kpi_calculator.py
│   ├── report_generator.py
│   ├── data_processor.py
│   ├── views.py
│   ├── urls.py
│   └── tests.py
│
├── notifications/
│   ├── __init__.py
│   ├── tasks.py
│   ├── email_sender.py
│   └── utils.py
│
├── static/
│   ├── css/
│   ├── js/
│   └── images/
│
├── media/
│   └── book_covers/
│
└── templates/
    ├── base.html
    ├── dashboard/
    └── admin/
```

---

## Complete Implementation Files

### 1. Django Settings Configuration

```python
# libris_core/settings.py
import os
from pathlib import Path
from dotenv import load_dotenv

load_dotenv()

BASE_DIR = Path(__file__).resolve().parent.parent

SECRET_KEY = os.getenv('SECRET_KEY', 'your-secret-key-change-in-production')
DEBUG = os.getenv('DEBUG', 'True') == 'True'
ALLOWED_HOSTS = os.getenv('ALLOWED_HOSTS', 'localhost,127.0.0.1').split(',')

# Application definition
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    
    # Third-party apps
    'rest_framework',
    'rest_framework.authtoken',
    'corsheaders',
    'django_filters',
    
    # Local apps
    'authentication.apps.AuthenticationConfig',
    'books.apps.BooksConfig',
    'transactions.apps.TransactionsConfig',
    'analytics.apps.AnalyticsConfig',
    'notifications.apps.NotificationsConfig',
]

MIDDLEWARE = [
    'django.middleware.security.SecurityMiddleware',
    'corsheaders.middleware.CorsMiddleware',
    'django.contrib.sessions.middleware.SessionMiddleware',
    'django.middleware.common.CommonMiddleware',
    'django.middleware.csrf.CsrfViewMiddleware',
    'django.contrib.auth.middleware.AuthenticationMiddleware',
    'django.contrib.messages.middleware.MessageMiddleware',
    'django.middleware.clickjacking.XFrameOptionsMiddleware',
]

ROOT_URLCONF = 'libris_core.urls'

TEMPLATES = [
    {
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        'DIRS': [BASE_DIR / 'templates'],
        'APP_DIRS': True,
        'OPTIONS': {
            'context_processors': [
                'django.template.context_processors.debug',
                'django.template.context_processors.request',
                'django.contrib.auth.context_processors.auth',
                'django.contrib.messages.context_processors.messages',
            ],
        },
    },
]

WSGI_APPLICATION = 'libris_core.wsgi.application'

# Database
DATABASES = {
    'default': {
        'ENGINE': 'django.db.backends.postgresql',
        'NAME': os.getenv('DB_NAME', 'libris_core'),
        'USER': os.getenv('DB_USER', 'postgres'),
        'PASSWORD': os.getenv('DB_PASSWORD', 'password'),
        'HOST': os.getenv('DB_HOST', 'localhost'),
        'PORT': os.getenv('DB_PORT', '5432'),
    }
}

# Custom User Model
AUTH_USER_MODEL = 'authentication.User'

# Password validation
AUTH_PASSWORD_VALIDATORS = [
    {'NAME': 'django.contrib.auth.password_validation.UserAttributeSimilarityValidator'},
    {'NAME': 'django.contrib.auth.password_validation.MinimumLengthValidator'},
    {'NAME': 'django.contrib.auth.password_validation.CommonPasswordValidator'},
    {'NAME': 'django.contrib.auth.password_validation.NumericPasswordValidator'},
]

# Internationalization
LANGUAGE_CODE = 'en-us'
TIME_ZONE = 'UTC'
USE_I18N = True
USE_TZ = True

# Static files (CSS, JavaScript, Images)
STATIC_URL = 'static/'
STATIC_ROOT = BASE_DIR / 'staticfiles'
STATICFILES_DIRS = [BASE_DIR / 'static']

# Media files
MEDIA_URL = 'media/'
MEDIA_ROOT = BASE_DIR / 'media'

# Default primary key field type
DEFAULT_AUTO_FIELD = 'django.db.models.BigAutoField'

# REST Framework
REST_FRAMEWORK = {
    'DEFAULT_AUTHENTICATION_CLASSES': [
        'rest_framework.authentication.TokenAuthentication',
        'rest_framework.authentication.SessionAuthentication',
    ],
    'DEFAULT_PERMISSION_CLASSES': [
        'rest_framework.permissions.IsAuthenticated',
    ],
    'DEFAULT_FILTER_BACKENDS': [
        'django_filters.rest_framework.DjangoFilterBackend',
        'rest_framework.filters.SearchFilter',
        'rest_framework.filters.OrderingFilter',
    ],
    'DEFAULT_PAGINATION_CLASS': 'rest_framework.pagination.PageNumberPagination',
    'PAGE_SIZE': 20,
}

# CORS Settings
CORS_ALLOWED_ORIGINS = [
    "http://localhost:3000",
    "http://localhost:5173",
    "http://127.0.0.1:3000",
]

# Celery Configuration
CELERY_BROKER_URL = os.getenv('REDIS_URL', 'redis://localhost:6379/0')
CELERY_RESULT_BACKEND = os.getenv('REDIS_URL', 'redis://localhost:6379/0')
CELERY_ACCEPT_CONTENT = ['json']
CELERY_TASK_SERIALIZER = 'json'
CELERY_RESULT_SERIALIZER = 'json'
CELERY_TIMEZONE = TIME_ZONE

# Email Configuration
EMAIL_BACKEND = 'django.core.mail.backends.smtp.EmailBackend'
EMAIL_HOST = os.getenv('EMAIL_HOST', 'smtp.gmail.com')
EMAIL_PORT = int(os.getenv('EMAIL_PORT', '587'))
EMAIL_USE_TLS = os.getenv('EMAIL_USE_TLS', 'True') == 'True'
EMAIL_HOST_USER = os.getenv('EMAIL_HOST_USER', '')
EMAIL_HOST_PASSWORD = os.getenv('EMAIL_HOST_PASSWORD', '')
DEFAULT_FROM_EMAIL = os.getenv('DEFAULT_FROM_EMAIL', 'noreply@libriscore.com')

# Fine Configuration
FINE_RATE_PER_DAY = 0.50  # $0.50 per day
DUE_DATE_DAYS = 14  # Books due in 14 days
REMINDER_DAYS_BEFORE = 3  # Send reminder 3 days before due date
```

### 2. Complete Models

```python
# authentication/models.py
from django.contrib.auth.models import AbstractUser
from django.db import models
import pyotp

class User(AbstractUser):
    """Extended User model with library-specific fields"""
    
    USER_TYPE_CHOICES = [
        ('user', 'User'),
        ('admin', 'Admin'),
    ]
    
    user_type = models.CharField(
        max_length=10, 
        choices=USER_TYPE_CHOICES, 
        default='user',
        db_index=True
    )
    phone_number = models.CharField(max_length=15, blank=True)
    address = models.TextField(blank=True)
    is_mfa_enabled = models.BooleanField(default=False)
    mfa_secret = models.CharField(max_length=32, blank=True)
    profile_image = models.ImageField(upload_to='profiles/', blank=True, null=True)
    date_of_birth = models.DateField(blank=True, null=True)
    membership_date = models.DateField(auto_now_add=True)
    total_books_borrowed = models.IntegerField(default=0)
    total_fines_paid = models.DecimalField(max_digits=10, decimal_places=2, default=0.00)
    is_active_member = models.BooleanField(default=True)
    
    class Meta:
        db_table = 'users'
        ordering = ['-date_joined']
        indexes = [
            models.Index(fields=['user_type', 'is_active']),
            models.Index(fields=['email']),
        ]
    
    def __str__(self):
        return f"{self.username} ({self.get_user_type_display()})"
    
    def generate_mfa_secret(self):
        """Generate MFA secret key"""
        self.mfa_secret = pyotp.random_base32()
        self.save()
        return self.mfa_secret
    
    def verify_mfa_code(self, code):
        """Verify MFA code"""
        if not self.is_mfa_enabled or not self.mfa_secret:
            return False
        totp = pyotp.TOTP(self.mfa_secret)
        return totp.verify(code)
    
    def get_mfa_qr_uri(self):
        """Get MFA QR code URI"""
        if not self.mfa_secret:
            self.generate_mfa_secret()
        totp = pyotp.TOTP(self.mfa_secret)
        return totp.provisioning_uri(
            name=self.email,
            issuer_name='Libris Core'
        )
```

```python
# books/models.py
from django.db import models
from django.core.validators import MinValueValidator
from django.utils.text import slugify

class Book(models.Model):
    """Book model for library inventory"""
    
    GENRE_CHOICES = [
        ('fiction', 'Fiction'),
        ('non_fiction', 'Non-Fiction'),
        ('science', 'Science'),
        ('history', 'History'),
        ('biography', 'Biography'),
        ('technology', 'Technology'),
        ('art', 'Art'),
        ('poetry', 'Poetry'),
        ('drama', 'Drama'),
        ('other', 'Other'),
    ]
    
    title = models.CharField(max_length=255, db_index=True)
    author = models.CharField(max_length=255, db_index=True)
    isbn = models.CharField(max_length=13, unique=True, db_index=True)
    genre = models.CharField(max_length=50, choices=GENRE_CHOICES, db_index=True)
    quantity = models.IntegerField(default=1, validators=[MinValueValidator(0)])
    available = models.IntegerField(default=1, validators=[MinValueValidator(0)])
    publish_date = models.DateField()
    publisher = models.CharField(max_length=255, blank=True)
    language = models.CharField(max_length=50, default='English')
    pages = models.IntegerField(blank=True, null=True)
    cover_url = models.URLField(blank=True)
    cover_image = models.ImageField(upload_to='book_covers/', blank=True, null=True)
    description = models.TextField(blank=True)
    slug = models.SlugField(max_length=255, unique=True, blank=True)
    avg_rating = models.DecimalField(max_digits=3, decimal_places=2, default=0.00)
    total_ratings = models.IntegerField(default=0)
    total_borrows = models.IntegerField(default=0)
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)
    is_active = models.BooleanField(default=True)
    
    class Meta:
        db_table = 'books'
        ordering = ['-created_at']
        indexes = [
            models.Index(fields=['title', 'author']),
            models.Index(fields=['genre', 'is_active']),
            models.Index(fields=['isbn']),
        ]
    
    def __str__(self):
        return f"{self.title} by {self.author}"
    
    def save(self, *args, **kwargs):
        if not self.slug:
            self.slug = slugify(f"{self.title}-{self.isbn}")
        super().save(*args, **kwargs)
    
    def is_available(self):
        """Check if book is available for borrowing"""
        return self.available > 0 and self.is_active
    
    def borrow(self):
        """Decrease available count when borrowed"""
        if self.available > 0:
            self.available -= 1
            self.total_borrows += 1
            self.save()
            return True
        return False
    
    def return_book(self):
        """Increase available count when returned"""
        if self.available < self.quantity:
            self.available += 1
            self.save()
            return True
        return False


class Review(models.Model):
    """Book review and rating model"""
    
    user = models.ForeignKey('authentication.User', on_delete=models.CASCADE, related_name='reviews')
    book = models.ForeignKey(Book, on_delete=models.CASCADE, related_name='reviews')
    rating = models.IntegerField(validators=[MinValueValidator(1), MaxValueValidator(5)])
    review = models.TextField(blank=True)
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)
    
    class Meta:
        db_table = 'reviews'
        unique_together = ['user', 'book']
        ordering = ['-created_at']
    
    def __str__(self):
        return f"{self.user.username} - {self.book.title} ({self.rating}★)"
    
    def save(self, *args, **kwargs):
        super().save(*args, **kwargs)
        # Update book's average rating
        self.book.update_rating()


class Category(models.Model):
    """Custom categories for organizing books"""
    
    name = models.CharField(max_length=100, unique=True)
    description = models.TextField(blank=True)
    books = models.ManyToManyField(Book, related_name='categories', blank=True)
    created_by = models.ForeignKey('authentication.User', on_delete=models.SET_NULL, null=True)
    created_at = models.DateTimeField(auto_now_add=True)
    
    class Meta:
        db_table = 'categories'
        verbose_name_plural = 'Categories'
        ordering = ['name']
    
    def __str__(self):
        return self.name
```

```python
# transactions/models.py
from django.db import models
from django.utils import timezone
from datetime import timedelta
from django.conf import settings

class Transaction(models.Model):
    """Transaction model for book borrowing/returning"""
    
    STATUS_CHOICES = [
        ('borrowed', 'Borrowed'),
        ('returned', 'Returned'),
        ('overdue', 'Overdue'),
    ]
    
    user = models.ForeignKey(
        settings.AUTH_USER_MODEL, 
        on_delete=models.CASCADE, 
        related_name='transactions'
    )
    book = models.ForeignKey('books.Book', on_delete=models.CASCADE, related_name='transactions')
    borrow_date = models.DateTimeField(default=timezone.now)
    due_date = models.DateTimeField()
    return_date = models.DateTimeField(null=True, blank=True)
    status = models.CharField(max_length=20, choices=STATUS_CHOICES, default='borrowed')
    fine_amount = models.DecimalField(max_digits=10, decimal_places=2, default=0.00)
    fine_paid = models.BooleanField(default=False)
    notes = models.TextField(blank=True)
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)
    
    class Meta:
        db_table = 'transactions'
        ordering = ['-borrow_date']
        indexes = [
            models.Index(fields=['user', 'status']),
            models.Index(fields=['book', 'status']),
            models.Index(fields=['due_date']),
        ]
    
    def __str__(self):
        return f"{self.user.username} - {self.book.title} ({self.status})"
    
    def save(self, *args, **kwargs):
        # Set due date if not provided
        if not self.due_date:
            self.due_date = self.borrow_date + timedelta(days=settings.DUE_DATE_DAYS)
        
        # Update status based on dates
        if not self.return_date and timezone.now() > self.due_date:
            self.status = 'overdue'
        elif self.return_date:
            self.status = 'returned'
        
        super().save(*args, **kwargs)
    
    def calculate_fine(self):
        """Calculate fine amount based on overdue days"""
        if self.return_date:
            if self.return_date > self.due_date:
                days_overdue = (self.return_date - self.due_date).days
                self.fine_amount = days_overdue * settings.FINE_RATE_PER_DAY
        elif timezone.now() > self.due_date:
            days_overdue = (timezone.now() - self.due_date).days
            self.fine_amount = days_overdue * settings.FINE_RATE_PER_DAY
        else:
            self.fine_amount = 0.00
        
        self.save()
        return self.fine_amount
    
    def return_book(self):
        """Process book return"""
        if self.status == 'returned':
            return False
        
        self.return_date = timezone.now()
        self.status = 'returned'
        self.calculate_fine()
        self.save()
        
        # Update book availability
        self.book.return_book()
        
        return True
    
    def is_overdue(self):
        """Check if transaction is overdue"""
        if self.return_date:
            return False
        return timezone.now() > self.due_date
    
    def days_overdue(self):
        """Calculate days overdue"""
        if not self.is_overdue():
            return 0
        return (timezone.now() - self.due_date).days


class Fine(models.Model):
    """Fine payment tracking"""
    
    transaction = models.ForeignKey(Transaction, on_delete=models.CASCADE, related_name='fine_payments')
    amount = models.DecimalField(max_digits=10, decimal_places=2)
    paid = models.BooleanField(default=False)
    payment_date = models.DateTimeField(null=True, blank=True)
    payment_method = models.CharField(max_length=50, blank=True)
    notes = models.TextField(blank=True)
    created_at = models.DateTimeField(auto_now_add=True)
    
    class Meta:
        db_table = 'fines'
        ordering = ['-created_at']
    
    def __str__(self):
        return f"Fine ${self.amount} - {self.transaction.user.username}"
    
    def mark_paid(self, payment_method=''):
        """Mark fine as paid"""
        self.paid = True
        self.payment_date = timezone.now()
        self.payment_method = payment_method
        self.save()
        
        # Update transaction
        self.transaction.fine_paid = True
        self.transaction.save()
        
        # Update user total fines
        user = self.transaction.user
        user.total_fines_paid += self.amount
        user.save()
```

### 3. Analytics with Pandas Implementation

```python
# analytics/kpi_calculator.py
import pandas as pd
import numpy as np
from django.db.models import Count, Avg, Sum, F, Q
from django.utils import timezone
from datetime import datetime, timedelta
from transactions.models import Transaction
from authentication.models import User
from books.models import Book, Review

class KPICalculator:
    """Calculate Key Performance Indicators using Pandas"""
    
    def __init__(self, start_date=None, end_date=None):
        self.start_date = start_date or (timezone.now() - timedelta(days=30))
        self.end_date = end_date or timezone.now()
    
    def get_user_metrics(self):
        """Calculate user-related KPIs"""
        # Total users
        total_users = User.objects.filter(user_type='user').count()
        
        # Active users (borrowed at least one book)
        active_users = Transaction.objects.filter(
            borrow_date__gte=self.start_date,
            borrow_date__lte=self.end_date
        ).values('user').distinct().count()
        
        # New users
        new_users = User.objects.filter(
            date_joined__gte=self.start_date,
            date_joined__lte=self.end_date,
            user_type='user'
        ).count()
        
        # Calculate growth rate
        period_length = (self.end_date - self.start_date).days
        previous_start = self.start_date - timedelta(days=period_length)
        previous_users = User.objects.filter(
            date_joined__gte=previous_start,
            date_joined__lt=self.start_date,
            user_type='user'
        ).count()
        
        growth_rate = ((new_users - previous_users) / previous_users * 100) if previous_users > 0 else 0
        
        # Active rate
        active_rate = (active_users / total_users * 100) if total_users > 0 else 0
        
        # Churn rate (users who haven't borrowed in 90 days)
        ninety_days_ago = timezone.now() - timedelta(days=90)
        inactive_users = User.objects.filter(
            user_type='user',
            is_active=True
        ).exclude(
            transactions__borrow_date__gte=ninety_days_ago
        ).count()
        churn_rate = (inactive_users / total_users * 100) if total_users > 0 else 0
        
        # Average books per user
        user_borrow_counts = Transaction.objects.filter(
            borrow_date__gte=self.start_date,
            borrow_date__lte=self.end_date
        ).values('user').annotate(count=Count('id'))
        
        if user_borrow_counts:
            df = pd.DataFrame(list(user_borrow_counts))
            avg_books_per_user = df['count'].mean()
        else:
            avg_books_per_user = 0
        
        return {
            'total_users': total_users,
            'active_users': active_users,
            'new_users': new_users,
            'growth_rate': round(growth_rate, 2),
            'active_rate': round(active_rate, 2),
            'churn_rate': round(churn_rate, 2),
            'avg_books_per_user': round(avg_books_per_user, 2)
        }
    
    def get_book_metrics(self):
        """Calculate book-related KPIs"""
        total_books = Book.objects.filter(is_active=True).count()
        total_inventory = Book.objects.filter(is_active=True).aggregate(
            Sum('quantity')
        )['quantity__sum'] or 0
        
        available_books = Book.objects.filter(is_active=True).aggregate(
            Sum('available')
        )['available__sum'] or 0
        
        borrowed_books = Transaction.objects.filter(
            status='borrowed'
        ).count()
        
        overdue_books = Transaction.objects.filter(
            status='overdue'
        ).count()
        
        # Circulation rate
        circulation_rate = (borrowed_books / total_inventory * 100) if total_inventory > 0 else 0
        
        # Average borrow duration using Pandas
        returned_transactions = Transaction.objects.filter(
            return_date__isnull=False,
            borrow_date__gte=self.start_date
        ).values('borrow_date', 'return_date')
        
        if returned_transactions:
            df = pd.DataFrame(list(returned_transactions))
            df['borrow_date'] = pd.to_datetime(df['borrow_date'])
            df['return_date'] = pd.to_datetime(df['return_date'])
            df['duration'] = (df['return_date'] - df['borrow_date']).dt.days
            avg_duration = df['duration'].mean()
        else:
            avg_duration = 0
        
        # Return rate (on-time returns)
        total_returns = Transaction.objects.filter(
            return_date__isnull=False,
            borrow_date__gte=self.start_date
        ).count()
        
        on_time_returns = Transaction.objects.filter(
            return_date__isnull=False,
            borrow_date__gte=self.start_date,
            return_date__lte=F('due_date')
        ).count()
        
        return_rate = (on_time_returns / total_returns * 100) if total_returns > 0 else 0
        
        # Most borrowed genre
        genre_data = Transaction.objects.filter(
            borrow_date__gte=self.start_date
        ).values('book__genre').annotate(count=Count('id')).order_by('-count')
        
        most_borrowed_genre = genre_data[0]['book__genre'] if genre_data else 'N/A'
        
        return {
            'total_books': total_books,
            'total_inventory': total_inventory,
            'available_books': available_books,
            'borrowed_books': borrowed_books,
            'overdue_books': overdue_books,
            'circulation_rate': round(circulation_rate, 2),
            'avg_borrow_duration': round(avg_duration, 2),
            'return_rate': round(return_rate, 2),
            'most_borrowed_genre': most_borrowed_genre
        }
    
    def get_financial_metrics(self):
        """Calculate financial KPIs"""
        transactions = Transaction.objects.filter(
            borrow_date__gte=self.start_date,
            borrow_date__lte=self.end_date
        )
        
        total_fines = transactions.aggregate(Sum('fine_amount'))['fine_amount__sum'] or 0
        
        # Collected fines
        collected_fines = transactions.filter(
            fine_paid=True
        ).aggregate(Sum('fine_amount'))['fine_amount__sum'] or 0
        
        # Pending fines
        pending_fines = total_fines - collected_fines
        
        # Collection rate
        collection_rate = (collected_fines / total_fines * 100) if total_fines > 0 else 0
        
        # Average fine amount
        fines_with_amount = transactions.filter(fine_amount__gt=0)
        avg_fine = fines_with_amount.aggregate(Avg('fine_amount'))['fine_amount__avg'] or 0
        
        # Monthly growth
        period_length = (self.end_date - self.start_date).days
        previous_start = self.start_date - timedelta(days=period_length)
        previous_fines = Transaction.objects.filter(
            borrow_date__gte=previous_start,
            borrow_date__lt=self.start_date
        ).aggregate(Sum('fine_amount'))['fine_amount__sum'] or 0
        
        monthly_growth = ((total_fines - previous_fines) / previous_fines * 100) if previous_fines > 0 else 0
        
        return {
            'total_fines': float(total_fines),
            'collected_fines': float(collected_fines),
            'pending_fines': float(pending_fines),
            'collection_rate': round(collection_rate, 2),
            'avg_fine_amount': float(round(avg_fine, 2)),
            'monthly_growth': round(monthly_growth, 2)
        }
    
    def get_transaction_trends(self):
        """Get monthly transaction trends using Pandas"""
        transactions = Transaction.objects.filter(
            borrow_date__gte=self.start_date
        ).values('borrow_date', 'return_date', 'status')
        
        df = pd.DataFrame(list(transactions))
        
        if df.empty:
            return []
        
        df['borrow_date'] = pd.to_datetime(df['borrow_date'])
        df['month'] = df['borrow_date'].dt.strftime('%b')
        df['year'] = df['borrow_date'].dt.year
        
        # Group by month
        monthly_stats = df.groupby(['year', 'month']).agg({
            'borrow_date': 'count',
            'return_date': lambda x: x.notna().sum(),
        }).reset_index()
        
        monthly_stats.columns = ['year', 'month', 'borrowed', 'returned']
        
        # Calculate overdue
        overdue_df = df[df['status'] == 'overdue'].groupby(['year', 'month']).size().reset_index(name='overdue')
        monthly_stats = monthly_stats.merge(overdue_df, on=['year', 'month'], how='left')
        monthly_stats['overdue'] = monthly_stats['overdue'].fillna(0)
        
        return monthly_stats.to_dict('records')
    
    def get_genre_distribution(self):
        """Get genre distribution using Pandas"""
        books = Book.objects.filter(is_active=True).values('genre')
        df = pd.DataFrame(list(books))
        
        if df.empty:
            return []
        
        distribution = df['genre'].value_counts().reset_index()
        distribution.columns = ['genre', 'count']
        distribution['percentage'] = (distribution['count'] / distribution['count'].sum() * 100).round(2)
        
        return distribution.to_dict('records')
    
    def get_user_behavior_analysis(self):
        """Analyze user behavior patterns with Pandas"""
        transactions = Transaction.objects.all().values(
            'user_id', 'book__genre', 'borrow_date', 'return_date', 'fine_amount'
        )
        
        df = pd.DataFrame(list(transactions))
        
        if df.empty:
            return {}
        
        # User borrowing frequency
        user_stats = df.groupby('user_id').agg({
            'book__genre': 'count',
            'fine_amount': 'sum'
        }).rename(columns={
            'book__genre': 'total_borrows',
            'fine_amount': 'total_fines'
        })
        
        # Genre preferences
        genre_prefs = df.groupby(['user_id', 'book__genre']).size().reset_index(name='count')
        top_genres_per_user = genre_prefs.sort_values(['user_id', 'count'], ascending=[True, False])
        
        return {
            'user_statistics': user_stats.describe().to_dict(),
            'top_genre_preferences': top_genres_per_user.head(20).to_dict('records'),
            'avg_borrows_per_user': user_stats['total_borrows'].mean(),
            'avg_fines_per_user': user_stats['total_fines'].mean()
        }
    
    def generate_comprehensive_report(self):
        """Generate comprehensive KPI report"""
        return {
            'user_metrics': self.get_user_metrics(),
            'book_metrics': self.get_book_metrics(),
            'financial_metrics': self.get_financial_metrics(),
            'transaction_trends': self.get_transaction_trends(),
            'genre_distribution': self.get_genre_distribution(),
            'user_behavior': self.get_user_behavior_analysis(),
            'report_period': {
                'start_date': self.start_date.strftime('%Y-%m-%d'),
                'end_date': self.end_date.strftime('%Y-%m-%d')
            },
            'generated_at': timezone.now().isoformat()
        }
```

This is a comprehensive implementation guide. The complete code continues with API views, serializers, Celery tasks, and more. Would you like me to continue with additional sections?
