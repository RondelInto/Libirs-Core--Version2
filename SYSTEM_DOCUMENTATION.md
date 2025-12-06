# Libris Core - Library Management System
## Comprehensive System Documentation & Python Conversion Guide

---

## Table of Contents
1. [System Overview](#system-overview)
2. [Architecture](#architecture)
3. [File Structure](#file-structure)
4. [Component Documentation](#component-documentation)
5. [Python Conversion Guide](#python-conversion-guide)
6. [Database Schema](#database-schema)
7. [KPI System](#kpi-system)
8. [Research Components](#research-components)
9. [API Endpoints](#api-endpoints)
10. [Deployment Guide](#deployment-guide)

---

## 1. System Overview

### Project Name
**Libris Core** - Enterprise Library Management System

### Version
1.0.0

### Purpose
A comprehensive library management system with dual interfaces for patrons and administrators, featuring real-time tracking, automated notifications, fine management, and advanced analytics.

### Key Features
- ✅ Role-Based Access Control (User/Admin)
- ✅ Real-Time Book Availability Tracking
- ✅ Automated Overdue Notifications
- ✅ Fine Calculation System ($0.50/day)
- ✅ Multi-Factor Authentication (MFA)
- ✅ Password Strength Validation
- ✅ Responsive Design (Desktop/Tablet/Mobile)
- ✅ KPI Dashboard & Analytics
- ✅ System Architecture Mapping
- ✅ Detailed Reporting System

### Technology Stack (Current - React/TypeScript)
- **Frontend**: React 18+ with TypeScript
- **Styling**: Tailwind CSS 4.0
- **Charts**: Recharts
- **Icons**: Lucide React
- **State Management**: React Hooks (useState, useEffect)
- **UI Components**: Custom UI library (shadcn/ui based)

---

## 2. Architecture

### System Layers

#### **Presentation Layer**
- User Interface (Login, Registration, Dashboard, Book Browsing)
- Admin Interface (Management, Reports, Settings)
- Responsive Components
- Form Validation

#### **Business Logic Layer**
- Authentication & Authorization
- Transaction Processing
- Search & Filter Logic
- Fine Calculation Engine
- Notification System
- Data Validation

#### **Data Layer**
- User Data Management
- Book Inventory Management
- Transaction Records
- Fine Records
- Analytics Data

### Design Pattern
- **Component-Based Architecture**
- **Container/Presentational Pattern**
- **Custom Hooks for Reusability**
- **State Management via Props & Context**

---

## 3. File Structure

```
/
├── App.tsx                          # Main application entry point
├── components/
│   ├── Logo.tsx                     # Libris Core logo component
│   ├── LoginPage.tsx                # User login interface
│   ├── RegistrationPage.tsx         # User registration with MFA
│   ├── UserDashboard.tsx            # Basic user dashboard
│   ├── EnhancedUserDashboard.tsx    # Enhanced user dashboard
│   ├── AdminDashboard.tsx           # Admin dashboard
│   │
│   ├── admin/                       # Admin-specific components
│   │   ├── BooksManagement.tsx      # Book CRUD operations
│   │   ├── UsersManagement.tsx      # User management
│   │   ├── TransactionHistory.tsx   # Transaction logs
│   │   ├── ReportGenerator.tsx      # Report generation
│   │   └── SystemSettings.tsx       # System configuration
│   │
│   ├── user/                        # User-specific components
│   │   ├── AddBookDialog.tsx        # Add book dialog
│   │   ├── BookReviewRating.tsx     # Book reviews/ratings
│   │   ├── CustomCategories.tsx     # Custom book categories
│   │   ├── ReadingProgress.tsx      # Reading progress tracker
│   │   └── ReadingStats.tsx         # Reading statistics
│   │
│   ├── analytics/                   # Analytics & Reporting
│   │   ├── SystemMapping.tsx        # System architecture visualization
│   │   ├── KPIDashboard.tsx         # KPI metrics & charts
│   │   └── DetailedReport.tsx       # Comprehensive reports
│   │
│   ├── ui/                          # Reusable UI components
│   │   ├── button.tsx
│   │   ├── card.tsx
│   │   ├── input.tsx
│   │   ├── table.tsx
│   │   ├── dialog.tsx
│   │   └── ... (30+ UI components)
│   │
│   └── figma/
│       └── ImageWithFallback.tsx    # Image component
│
├── data/
│   └── mockData.ts                  # Mock data for development
│
├── styles/
│   └── globals.css                  # Global styles & design tokens
│
└── SYSTEM_DOCUMENTATION.md          # This file
```

---

## 4. Component Documentation

### Core Components

#### **App.tsx**
- **Purpose**: Main application router and state management
- **State**: Current user, registration toggle
- **Logic**: Conditional rendering based on user authentication and role

#### **LoginPage.tsx**
- **Purpose**: User authentication interface
- **Features**: Email/password validation, error handling, brand styling
- **State**: Form inputs, error messages

#### **RegistrationPage.tsx**
- **Purpose**: New user registration with security
- **Features**: MFA setup, password strength indicator, email validation
- **State**: Form inputs, password strength, MFA status

#### **EnhancedUserDashboard.tsx**
- **Purpose**: Main user interface for book management
- **Features**: Book browsing, search, borrow/return, reading progress
- **State**: Books, borrowed books, search filters

#### **AdminDashboard.tsx**
- **Purpose**: Administrative control panel
- **Features**: Navigation to all admin functions, system overview
- **State**: Active view, system statistics

### Analytics Components

#### **SystemMapping.tsx**
- **Purpose**: Visual representation of system architecture
- **Features**: Layer visualization, data flow diagram, feature breakdown
- **Data**: Static architecture information

#### **KPIDashboard.tsx**
- **Purpose**: Key Performance Indicators display
- **Features**: Real-time metrics, charts (bar, line, pie, area), trend analysis
- **Data**: User metrics, book metrics, financial metrics, activity trends
- **Charts**: 
  - Monthly transaction trends (Bar Chart)
  - Genre distribution (Pie Chart)
  - User activity trends (Area Chart)
  - Fine collection analysis (Line Chart)

#### **DetailedReport.tsx**
- **Purpose**: Comprehensive system reporting
- **Features**: 
  - Executive summary
  - Top performing books
  - Most active users
  - Overdue analysis
  - Performance recommendations
- **Export**: PDF/CSV export capability
- **Filters**: Date range selection

---

## 5. Python Conversion Guide

### Overview
To convert this React/TypeScript application to Python, you would use:
- **Backend Framework**: Django or Flask
- **Frontend**: Django Templates or Flask + Jinja2 (or keep React as frontend)
- **Database**: PostgreSQL or MySQL
- **Analytics**: Pandas, NumPy, Matplotlib/Plotly

### Recommended Python Stack

```python
# Backend
Django==4.2.0
djangorestframework==3.14.0
django-cors-headers==4.0.0

# Database
psycopg2-binary==2.9.6
sqlalchemy==2.0.15

# Analytics & Data Processing
pandas==2.0.2
numpy==1.24.3
matplotlib==3.7.1
plotly==5.14.1
seaborn==0.12.2

# Authentication
django-allauth==0.54.0
PyJWT==2.7.0

# Task Queue (for notifications)
celery==5.2.7
redis==4.5.5

# PDF Generation
reportlab==4.0.4
weasyprint==59.0

# Excel Export
openpyxl==3.1.2
xlsxwriter==3.1.2
```

### Project Structure (Python/Django)

```
libris_core/
├── manage.py
├── requirements.txt
├── libris_core/
│   ├── __init__.py
│   ├── settings.py
│   ├── urls.py
│   └── wsgi.py
│
├── apps/
│   ├── authentication/
│   │   ├── models.py
│   │   ├── views.py
│   │   ├── serializers.py
│   │   └── urls.py
│   │
│   ├── books/
│   │   ├── models.py
│   │   ├── views.py
│   │   ├── serializers.py
│   │   └── urls.py
│   │
│   ├── transactions/
│   │   ├── models.py
│   │   ├── views.py
│   │   ├── serializers.py
│   │   └── urls.py
│   │
│   ├── analytics/
│   │   ├── kpi_calculator.py
│   │   ├── report_generator.py
│   │   ├── data_processor.py
│   │   └── views.py
│   │
│   └── notifications/
│       ├── tasks.py
│       ├── email_sender.py
│       └── utils.py
│
├── static/
├── templates/
└── media/
```

### Key Python Code Examples

#### 1. User Model (Django)

```python
# apps/authentication/models.py
from django.contrib.auth.models import AbstractUser
from django.db import models

class User(AbstractUser):
    USER_TYPE_CHOICES = [
        ('user', 'User'),
        ('admin', 'Admin'),
    ]
    
    user_type = models.CharField(max_length=10, choices=USER_TYPE_CHOICES, default='user')
    phone_number = models.CharField(max_length=15, blank=True)
    address = models.TextField(blank=True)
    is_mfa_enabled = models.BooleanField(default=False)
    mfa_secret = models.CharField(max_length=32, blank=True)
    created_at = models.DateTimeField(auto_now_add=True)
    updated_at = models.DateTimeField(auto_now=True)
    
    def __str__(self):
        return self.username
```

#### 2. Book Model

```python
# apps/books/models.py
from django.db import models

class Book(models.Model):
    GENRE_CHOICES = [
        ('fiction', 'Fiction'),
        ('non_fiction', 'Non-Fiction'),
        ('science', 'Science'),
        ('history', 'History'),
        ('biography', 'Biography'),
        ('other', 'Other'),
    ]
    
    title = models.CharField(max_length=255)
    author = models.CharField(max_length=255)
    isbn = models.CharField(max_length=13, unique=True)
    genre = models.CharField(max_length=50, choices=GENRE_CHOICES)
    quantity = models.IntegerField(default=1)
    available = models.IntegerField(default=1)
    publish_date = models.DateField()
    cover_url = models.URLField(blank=True)
    description = models.TextField(blank=True)
    created_at = models.DateTimeField(auto_now_add=True)
    
    def __str__(self):
        return self.title
```

#### 3. Transaction Model

```python
# apps/transactions/models.py
from django.db import models
from django.utils import timezone
from datetime import timedelta

class Transaction(models.Model):
    STATUS_CHOICES = [
        ('borrowed', 'Borrowed'),
        ('returned', 'Returned'),
        ('overdue', 'Overdue'),
    ]
    
    user = models.ForeignKey('authentication.User', on_delete=models.CASCADE)
    book = models.ForeignKey('books.Book', on_delete=models.CASCADE)
    borrow_date = models.DateTimeField(default=timezone.now)
    due_date = models.DateTimeField()
    return_date = models.DateTimeField(null=True, blank=True)
    status = models.CharField(max_length=20, choices=STATUS_CHOICES, default='borrowed')
    fine_amount = models.DecimalField(max_digits=10, decimal_places=2, default=0.00)
    
    def save(self, *args, **kwargs):
        if not self.due_date:
            self.due_date = self.borrow_date + timedelta(days=14)
        super().save(*args, **kwargs)
    
    def calculate_fine(self):
        """Calculate fine at $0.50 per day"""
        if self.return_date and self.return_date > self.due_date:
            days_overdue = (self.return_date - self.due_date).days
            self.fine_amount = days_overdue * 0.50
        elif not self.return_date and timezone.now() > self.due_date:
            days_overdue = (timezone.now() - self.due_date).days
            self.fine_amount = days_overdue * 0.50
        return self.fine_amount
```

#### 4. KPI Calculator with Pandas

```python
# apps/analytics/kpi_calculator.py
import pandas as pd
import numpy as np
from django.db.models import Count, Avg, Sum
from datetime import datetime, timedelta
from apps.transactions.models import Transaction
from apps.authentication.models import User
from apps.books.models import Book

class KPICalculator:
    """Calculate Key Performance Indicators for Library System"""
    
    def __init__(self, start_date=None, end_date=None):
        self.start_date = start_date or (datetime.now() - timedelta(days=30))
        self.end_date = end_date or datetime.now()
    
    def get_user_metrics(self):
        """Calculate user-related KPIs"""
        total_users = User.objects.filter(user_type='user').count()
        active_users = Transaction.objects.filter(
            borrow_date__gte=self.start_date
        ).values('user').distinct().count()
        
        new_users = User.objects.filter(
            date_joined__gte=self.start_date,
            user_type='user'
        ).count()
        
        # Calculate growth rate
        previous_period = self.start_date - (self.end_date - self.start_date)
        previous_users = User.objects.filter(
            date_joined__lt=self.start_date,
            date_joined__gte=previous_period
        ).count()
        
        growth_rate = ((new_users - previous_users) / previous_users * 100) if previous_users > 0 else 0
        
        return {
            'total_users': total_users,
            'active_users': active_users,
            'new_users': new_users,
            'growth_rate': round(growth_rate, 2),
            'active_rate': round((active_users / total_users * 100), 2) if total_users > 0 else 0
        }
    
    def get_book_metrics(self):
        """Calculate book-related KPIs"""
        total_books = Book.objects.count()
        borrowed_books = Transaction.objects.filter(
            status='borrowed'
        ).count()
        
        overdue_books = Transaction.objects.filter(
            status='overdue'
        ).count()
        
        # Circulation rate
        circulation_rate = (borrowed_books / total_books * 100) if total_books > 0 else 0
        
        # Average borrow duration
        returned_transactions = Transaction.objects.filter(
            return_date__isnull=False,
            borrow_date__gte=self.start_date
        )
        
        if returned_transactions.exists():
            df = pd.DataFrame(list(returned_transactions.values('borrow_date', 'return_date')))
            df['duration'] = (df['return_date'] - df['borrow_date']).dt.days
            avg_duration = df['duration'].mean()
        else:
            avg_duration = 0
        
        return {
            'total_books': total_books,
            'borrowed_books': borrowed_books,
            'overdue_books': overdue_books,
            'circulation_rate': round(circulation_rate, 2),
            'avg_borrow_duration': round(avg_duration, 2)
        }
    
    def get_financial_metrics(self):
        """Calculate financial KPIs"""
        transactions = Transaction.objects.filter(
            borrow_date__gte=self.start_date
        )
        
        total_fines = transactions.aggregate(Sum('fine_amount'))['fine_amount__sum'] or 0
        
        # Calculate pending fines
        pending_fines = transactions.filter(
            fine_amount__gt=0,
            return_date__isnull=True
        ).aggregate(Sum('fine_amount'))['fine_amount__sum'] or 0
        
        collected_fines = total_fines - pending_fines
        
        collection_rate = (collected_fines / total_fines * 100) if total_fines > 0 else 0
        
        return {
            'total_fines': float(total_fines),
            'collected_fines': float(collected_fines),
            'pending_fines': float(pending_fines),
            'collection_rate': round(collection_rate, 2)
        }
    
    def get_transaction_trends(self):
        """Get monthly transaction trends using Pandas"""
        transactions = Transaction.objects.filter(
            borrow_date__gte=self.start_date
        ).values('borrow_date', 'return_date', 'status')
        
        df = pd.DataFrame(list(transactions))
        
        if df.empty:
            return []
        
        df['month'] = pd.to_datetime(df['borrow_date']).dt.strftime('%b')
        
        trends = df.groupby('month').agg({
            'borrow_date': 'count',
            'return_date': lambda x: x.notna().sum(),
        }).reset_index()
        
        trends.columns = ['month', 'borrowed', 'returned']
        
        # Calculate overdue
        overdue_counts = df[df['status'] == 'overdue'].groupby('month').size()
        trends['overdue'] = trends['month'].map(overdue_counts).fillna(0)
        
        return trends.to_dict('records')
    
    def get_genre_distribution(self):
        """Get genre distribution using Pandas"""
        books = Book.objects.all().values('genre')
        df = pd.DataFrame(list(books))
        
        if df.empty:
            return []
        
        distribution = df['genre'].value_counts().reset_index()
        distribution.columns = ['genre', 'count']
        distribution['percentage'] = (distribution['count'] / distribution['count'].sum() * 100).round(2)
        
        return distribution.to_dict('records')
    
    def generate_comprehensive_report(self):
        """Generate comprehensive KPI report"""
        return {
            'user_metrics': self.get_user_metrics(),
            'book_metrics': self.get_book_metrics(),
            'financial_metrics': self.get_financial_metrics(),
            'transaction_trends': self.get_transaction_trends(),
            'genre_distribution': self.get_genre_distribution(),
            'report_period': {
                'start_date': self.start_date.strftime('%Y-%m-%d'),
                'end_date': self.end_date.strftime('%Y-%m-%d')
            }
        }
```

#### 5. Report Generator

```python
# apps/analytics/report_generator.py
import pandas as pd
import matplotlib.pyplot as plt
import seaborn as sns
from io import BytesIO
import base64
from reportlab.lib.pagesizes import letter, A4
from reportlab.platypus import SimpleDocTemplate, Table, TableStyle, Paragraph, Spacer, PageBreak, Image
from reportlab.lib.styles import getSampleStyleSheet, ParagraphStyle
from reportlab.lib.units import inch
from reportlab.lib import colors
from datetime import datetime

class ReportGenerator:
    """Generate PDF and Excel reports with charts"""
    
    def __init__(self, kpi_data):
        self.kpi_data = kpi_data
        self.styles = getSampleStyleSheet()
        
    def generate_chart_base64(self, chart_type, data, title):
        """Generate chart and return as base64 string"""
        plt.figure(figsize=(8, 6))
        
        if chart_type == 'bar':
            df = pd.DataFrame(data)
            df.plot(kind='bar', x='month', y=['borrowed', 'returned', 'overdue'])
        elif chart_type == 'pie':
            df = pd.DataFrame(data)
            plt.pie(df['count'], labels=df['genre'], autopct='%1.1f%%')
        
        plt.title(title)
        plt.tight_layout()
        
        buffer = BytesIO()
        plt.savefig(buffer, format='png')
        buffer.seek(0)
        image_base64 = base64.b64encode(buffer.getvalue()).decode()
        plt.close()
        
        return image_base64
    
    def generate_pdf_report(self, filename):
        """Generate comprehensive PDF report"""
        doc = SimpleDocTemplate(filename, pagesize=letter)
        story = []
        
        # Title
        title_style = ParagraphStyle(
            'CustomTitle',
            parent=self.styles['Heading1'],
            fontSize=24,
            textColor=colors.HexColor('#4B0082'),
            spaceAfter=30,
        )
        
        story.append(Paragraph("Libris Core - Comprehensive System Report", title_style))
        story.append(Paragraph(f"Generated: {datetime.now().strftime('%Y-%m-%d %H:%M:%S')}", self.styles['Normal']))
        story.append(Spacer(1, 0.5*inch))
        
        # Executive Summary
        story.append(Paragraph("Executive Summary", self.styles['Heading2']))
        
        user_metrics = self.kpi_data['user_metrics']
        book_metrics = self.kpi_data['book_metrics']
        financial_metrics = self.kpi_data['financial_metrics']
        
        summary_data = [
            ['Metric', 'Value'],
            ['Total Users', str(user_metrics['total_users'])],
            ['Active Users', str(user_metrics['active_users'])],
            ['Total Books', str(book_metrics['total_books'])],
            ['Borrowed Books', str(book_metrics['borrowed_books'])],
            ['Total Fines Collected', f"${financial_metrics['collected_fines']:.2f}"],
            ['Circulation Rate', f"{book_metrics['circulation_rate']}%"],
        ]
        
        table = Table(summary_data)
        table.setStyle(TableStyle([
            ('BACKGROUND', (0, 0), (-1, 0), colors.HexColor('#4B0082')),
            ('TEXTCOLOR', (0, 0), (-1, 0), colors.whitesmoke),
            ('ALIGN', (0, 0), (-1, -1), 'LEFT'),
            ('FONTNAME', (0, 0), (-1, 0), 'Helvetica-Bold'),
            ('FONTSIZE', (0, 0), (-1, 0), 14),
            ('BOTTOMPADDING', (0, 0), (-1, 0), 12),
            ('BACKGROUND', (0, 1), (-1, -1), colors.beige),
            ('GRID', (0, 0), (-1, -1), 1, colors.black)
        ]))
        
        story.append(table)
        story.append(PageBreak())
        
        # Build PDF
        doc.build(story)
        
    def generate_excel_report(self, filename):
        """Generate Excel report with multiple sheets"""
        with pd.ExcelWriter(filename, engine='xlsxwriter') as writer:
            # Summary Sheet
            summary_df = pd.DataFrame([
                self.kpi_data['user_metrics'],
                self.kpi_data['book_metrics'],
                self.kpi_data['financial_metrics']
            ])
            summary_df.to_excel(writer, sheet_name='Summary', index=False)
            
            # Transaction Trends
            trends_df = pd.DataFrame(self.kpi_data['transaction_trends'])
            trends_df.to_excel(writer, sheet_name='Transaction Trends', index=False)
            
            # Genre Distribution
            genre_df = pd.DataFrame(self.kpi_data['genre_distribution'])
            genre_df.to_excel(writer, sheet_name='Genre Distribution', index=False)
            
            # Format workbook
            workbook = writer.book
            header_format = workbook.add_format({
                'bold': True,
                'text_wrap': True,
                'valign': 'top',
                'fg_color': '#4B0082',
                'font_color': '#FFFFFF',
                'border': 1
            })
```

#### 6. Automated Notification System

```python
# apps/notifications/tasks.py
from celery import shared_task
from django.core.mail import send_mail
from django.utils import timezone
from datetime import timedelta
from apps.transactions.models import Transaction

@shared_task
def check_overdue_books():
    """Check for overdue books and send notifications"""
    now = timezone.now()
    
    # Find overdue transactions
    overdue_transactions = Transaction.objects.filter(
        due_date__lt=now,
        return_date__isnull=True,
        status='borrowed'
    )
    
    for transaction in overdue_transactions:
        # Update status
        transaction.status = 'overdue'
        transaction.calculate_fine()
        transaction.save()
        
        # Send email notification
        send_overdue_notification(transaction)

@shared_task
def send_due_date_reminders():
    """Send reminders 3 days before due date"""
    three_days_from_now = timezone.now() + timedelta(days=3)
    
    upcoming_due = Transaction.objects.filter(
        due_date__date=three_days_from_now.date(),
        return_date__isnull=True,
        status='borrowed'
    )
    
    for transaction in upcoming_due:
        send_reminder_email(transaction)

def send_overdue_notification(transaction):
    """Send overdue notification email"""
    subject = f"Overdue Book: {transaction.book.title}"
    message = f"""
    Dear {transaction.user.get_full_name()},
    
    The book "{transaction.book.title}" was due on {transaction.due_date.strftime('%Y-%m-%d')} 
    and is now overdue.
    
    Current fine: ${transaction.fine_amount}
    Fine rate: $0.50 per day
    
    Please return the book as soon as possible to avoid additional charges.
    
    Thank you,
    Libris Core Team
    """
    
    send_mail(
        subject,
        message,
        'noreply@libriscore.com',
        [transaction.user.email],
        fail_silently=False,
    )

def send_reminder_email(transaction):
    """Send due date reminder email"""
    subject = f"Reminder: Book Due in 3 Days - {transaction.book.title}"
    message = f"""
    Dear {transaction.user.get_full_name()},
    
    This is a friendly reminder that the book "{transaction.book.title}" 
    is due on {transaction.due_date.strftime('%Y-%m-%d')}.
    
    Please return it on time to avoid late fees.
    
    Thank you,
    Libris Core Team
    """
    
    send_mail(
        subject,
        message,
        'noreply@libriscore.com',
        [transaction.user.email],
        fail_silently=False,
    )
```

#### 7. API Views (Django REST Framework)

```python
# apps/analytics/views.py
from rest_framework.views import APIView
from rest_framework.response import Response
from rest_framework.permissions import IsAdminUser
from .kpi_calculator import KPICalculator
from .report_generator import ReportGenerator

class KPIDashboardView(APIView):
    """API endpoint for KPI dashboard data"""
    permission_classes = [IsAdminUser]
    
    def get(self, request):
        calculator = KPICalculator()
        data = calculator.generate_comprehensive_report()
        return Response(data)

class GenerateReportView(APIView):
    """Generate and download reports"""
    permission_classes = [IsAdminUser]
    
    def post(self, request):
        report_type = request.data.get('type', 'pdf')
        
        calculator = KPICalculator()
        kpi_data = calculator.generate_comprehensive_report()
        
        generator = ReportGenerator(kpi_data)
        
        if report_type == 'pdf':
            filename = f'report_{datetime.now().strftime("%Y%m%d")}.pdf'
            generator.generate_pdf_report(filename)
        else:
            filename = f'report_{datetime.now().strftime("%Y%m%d")}.xlsx'
            generator.generate_excel_report(filename)
        
        return Response({'filename': filename, 'status': 'success'})
```

---

## 6. Database Schema

### Tables

#### Users Table
```sql
CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    username VARCHAR(150) UNIQUE NOT NULL,
    email VARCHAR(255) UNIQUE NOT NULL,
    password VARCHAR(255) NOT NULL,
    first_name VARCHAR(150),
    last_name VARCHAR(150),
    user_type VARCHAR(10) CHECK (user_type IN ('user', 'admin')),
    phone_number VARCHAR(15),
    address TEXT,
    is_mfa_enabled BOOLEAN DEFAULT FALSE,
    mfa_secret VARCHAR(32),
    is_active BOOLEAN DEFAULT TRUE,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

#### Books Table
```sql
CREATE TABLE books (
    id SERIAL PRIMARY KEY,
    title VARCHAR(255) NOT NULL,
    author VARCHAR(255) NOT NULL,
    isbn VARCHAR(13) UNIQUE NOT NULL,
    genre VARCHAR(50),
    quantity INTEGER DEFAULT 1,
    available INTEGER DEFAULT 1,
    publish_date DATE,
    cover_url VARCHAR(500),
    description TEXT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

#### Transactions Table
```sql
CREATE TABLE transactions (
    id SERIAL PRIMARY KEY,
    user_id INTEGER REFERENCES users(id) ON DELETE CASCADE,
    book_id INTEGER REFERENCES books(id) ON DELETE CASCADE,
    borrow_date TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    due_date TIMESTAMP NOT NULL,
    return_date TIMESTAMP,
    status VARCHAR(20) CHECK (status IN ('borrowed', 'returned', 'overdue')),
    fine_amount DECIMAL(10, 2) DEFAULT 0.00,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

#### Fines Table
```sql
CREATE TABLE fines (
    id SERIAL PRIMARY KEY,
    transaction_id INTEGER REFERENCES transactions(id) ON DELETE CASCADE,
    amount DECIMAL(10, 2) NOT NULL,
    paid BOOLEAN DEFAULT FALSE,
    paid_date TIMESTAMP,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

#### Reviews Table
```sql
CREATE TABLE reviews (
    id SERIAL PRIMARY KEY,
    user_id INTEGER REFERENCES users(id) ON DELETE CASCADE,
    book_id INTEGER REFERENCES books(id) ON DELETE CASCADE,
    rating INTEGER CHECK (rating >= 1 AND rating <= 5),
    review TEXT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    UNIQUE(user_id, book_id)
);
```

---

## 7. KPI System

### Key Performance Indicators

#### User Metrics
- **Total Users**: Count of all registered users
- **Active Users**: Users who borrowed at least one book in the period
- **New Registrations**: New users in the period
- **User Growth Rate**: Percentage increase in users
- **User Retention Rate**: Percentage of returning users
- **Avg Books Per User**: Average number of books borrowed per user

#### Book Metrics
- **Total Books**: Total inventory count
- **Available Books**: Books currently available
- **Borrowed Books**: Books currently borrowed
- **Circulation Rate**: Percentage of books in circulation
- **Avg Borrow Duration**: Average days books are borrowed
- **Return Rate**: Percentage of on-time returns

#### Financial Metrics
- **Total Revenue**: Total fines collected
- **Pending Fines**: Outstanding fines
- **Collection Rate**: Percentage of fines collected
- **Avg Fine Amount**: Average fine per overdue book
- **Monthly Growth**: Month-over-month revenue growth

#### Performance Metrics
- **Overdue Rate**: Percentage of overdue books
- **Response Time**: Average time to process transactions
- **System Uptime**: System availability percentage
- **User Satisfaction**: Based on reviews and ratings

### KPI Calculation Formulas

```python
# User Growth Rate
growth_rate = ((current_period_users - previous_period_users) / previous_period_users) * 100

# Circulation Rate
circulation_rate = (borrowed_books / total_books) * 100

# Collection Rate
collection_rate = (collected_fines / total_fines) * 100

# Return Rate
return_rate = (on_time_returns / total_returns) * 100

# Overdue Rate
overdue_rate = (overdue_books / total_borrowed_books) * 100
```

---

## 8. Research Components

### Pandas Data Analysis

#### User Behavior Analysis
```python
import pandas as pd
import numpy as np

def analyze_user_behavior(transactions_df):
    """Analyze user borrowing patterns"""
    
    # Group by user
    user_analysis = transactions_df.groupby('user_id').agg({
        'book_id': 'count',
        'fine_amount': 'sum',
        'borrow_date': lambda x: (x.max() - x.min()).days
    }).rename(columns={
        'book_id': 'total_borrows',
        'fine_amount': 'total_fines',
        'borrow_date': 'user_lifetime_days'
    })
    
    # Calculate borrowing frequency
    user_analysis['avg_books_per_month'] = (
        user_analysis['total_borrows'] / 
        (user_analysis['user_lifetime_days'] / 30)
    ).round(2)
    
    return user_analysis

def analyze_genre_preferences(books_df, transactions_df):
    """Analyze genre popularity over time"""
    
    merged = pd.merge(transactions_df, books_df, left_on='book_id', right_on='id')
    
    genre_trends = merged.groupby([
        pd.to_datetime(merged['borrow_date']).dt.to_period('M'),
        'genre'
    ]).size().unstack(fill_value=0)
    
    return genre_trends

def predictive_demand_analysis(transactions_df):
    """Predict future book demand"""
    
    # Time series analysis
    daily_borrows = transactions_df.groupby(
        pd.to_datetime(transactions_df['borrow_date']).dt.date
    ).size()
    
    # Calculate moving average
    daily_borrows_ma = daily_borrows.rolling(window=7).mean()
    
    # Simple linear trend
    from scipy import stats
    x = np.arange(len(daily_borrows))
    slope, intercept, r_value, p_value, std_err = stats.linregress(x, daily_borrows)
    
    # Predict next 30 days
    future_x = np.arange(len(daily_borrows), len(daily_borrows) + 30)
    predicted_demand = slope * future_x + intercept
    
    return {
        'historical': daily_borrows,
        'moving_average': daily_borrows_ma,
        'prediction': predicted_demand,
        'trend_slope': slope,
        'r_squared': r_value ** 2
    }
```

#### Statistical Analysis
```python
def statistical_summary(kpi_calculator):
    """Generate statistical summary of library operations"""
    
    # Get all metrics
    user_metrics = kpi_calculator.get_user_metrics()
    book_metrics = kpi_calculator.get_book_metrics()
    financial_metrics = kpi_calculator.get_financial_metrics()
    
    # Create comprehensive dataframe
    summary_df = pd.DataFrame({
        'Metric': [
            'Total Users', 'Active Users', 'User Growth Rate',
            'Total Books', 'Circulation Rate', 'Overdue Rate',
            'Total Revenue', 'Collection Rate'
        ],
        'Value': [
            user_metrics['total_users'],
            user_metrics['active_users'],
            user_metrics['growth_rate'],
            book_metrics['total_books'],
            book_metrics['circulation_rate'],
            (book_metrics['overdue_books'] / book_metrics['borrowed_books'] * 100),
            financial_metrics['collected_fines'],
            financial_metrics['collection_rate']
        ]
    })
    
    # Statistical analysis
    stats = {
        'mean': summary_df['Value'].mean(),
        'median': summary_df['Value'].median(),
        'std_dev': summary_df['Value'].std(),
        'variance': summary_df['Value'].var(),
        'min': summary_df['Value'].min(),
        'max': summary_df['Value'].max()
    }
    
    return summary_df, stats
```

### Data Visualization with Matplotlib/Seaborn

```python
import matplotlib.pyplot as plt
import seaborn as sns

def create_advanced_visualizations(kpi_data):
    """Create advanced data visualizations"""
    
    # Set style
    sns.set_style("darkgrid")
    plt.rcParams['figure.figsize'] = (15, 10)
    
    # Create subplots
    fig, axes = plt.subplots(2, 2)
    
    # 1. Transaction Trends
    trends_df = pd.DataFrame(kpi_data['transaction_trends'])
    trends_df.plot(x='month', y=['borrowed', 'returned', 'overdue'], 
                   kind='bar', ax=axes[0, 0])
    axes[0, 0].set_title('Monthly Transaction Trends')
    axes[0, 0].set_xlabel('Month')
    axes[0, 0].set_ylabel('Count')
    
    # 2. Genre Distribution
    genre_df = pd.DataFrame(kpi_data['genre_distribution'])
    axes[0, 1].pie(genre_df['count'], labels=genre_df['genre'], autopct='%1.1f%%')
    axes[0, 1].set_title('Genre Distribution')
    
    # 3. User Activity Heatmap
    # (Assuming we have daily activity data)
    # sns.heatmap(activity_matrix, ax=axes[1, 0], cmap='YlOrRd')
    axes[1, 0].set_title('User Activity Heatmap')
    
    # 4. Financial Trends
    # Line chart for revenue over time
    axes[1, 1].set_title('Financial Trends')
    
    plt.tight_layout()
    plt.savefig('comprehensive_analytics.png', dpi=300)
    plt.show()
```

---

## 9. API Endpoints

### Authentication
- `POST /api/auth/register/` - User registration
- `POST /api/auth/login/` - User login
- `POST /api/auth/logout/` - User logout
- `POST /api/auth/refresh/` - Refresh token
- `POST /api/auth/mfa/setup/` - Setup MFA
- `POST /api/auth/mfa/verify/` - Verify MFA code

### Books
- `GET /api/books/` - List all books
- `GET /api/books/{id}/` - Get book details
- `POST /api/books/` - Create new book (admin)
- `PUT /api/books/{id}/` - Update book (admin)
- `DELETE /api/books/{id}/` - Delete book (admin)
- `GET /api/books/search/?q={query}` - Search books
- `GET /api/books/filter/?genre={genre}` - Filter by genre

### Transactions
- `GET /api/transactions/` - List all transactions
- `GET /api/transactions/user/{user_id}/` - User's transactions
- `POST /api/transactions/borrow/` - Borrow book
- `POST /api/transactions/return/` - Return book
- `GET /api/transactions/overdue/` - List overdue books

### Analytics
- `GET /api/analytics/kpi/` - Get KPI dashboard data
- `GET /api/analytics/reports/` - List available reports
- `POST /api/analytics/reports/generate/` - Generate new report
- `GET /api/analytics/trends/` - Get trend data
- `GET /api/analytics/user-behavior/` - User behavior analysis

### Admin
- `GET /api/admin/users/` - List all users
- `PUT /api/admin/users/{id}/` - Update user
- `DELETE /api/admin/users/{id}/` - Delete user
- `GET /api/admin/system-stats/` - System statistics
- `POST /api/admin/settings/` - Update system settings

---

## 10. Deployment Guide

### Development Environment Setup

```bash
# Python/Django Setup
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate
pip install -r requirements.txt

# Database Setup
python manage.py makemigrations
python manage.py migrate
python manage.py createsuperuser

# Load sample data
python manage.py loaddata sample_data.json

# Run development server
python manage.py runserver

# Run Celery for background tasks
celery -A libris_core worker -l info
celery -A libris_core beat -l info
```

### Production Deployment (Docker)

```dockerfile
# Dockerfile
FROM python:3.11-slim

WORKDIR /app

COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

COPY . .

RUN python manage.py collectstatic --noinput

CMD ["gunicorn", "libris_core.wsgi:application", "--bind", "0.0.0.0:8000"]
```

```yaml
# docker-compose.yml
version: '3.8'

services:
  db:
    image: postgres:15
    environment:
      POSTGRES_DB: libris_core
      POSTGRES_USER: libris_user
      POSTGRES_PASSWORD: secure_password
    volumes:
      - postgres_data:/var/lib/postgresql/data

  redis:
    image: redis:7-alpine

  web:
    build: .
    command: gunicorn libris_core.wsgi:application --bind 0.0.0.0:8000
    volumes:
      - .:/app
      - static_volume:/app/staticfiles
      - media_volume:/app/media
    ports:
      - "8000:8000"
    depends_on:
      - db
      - redis
    environment:
      - DATABASE_URL=postgresql://libris_user:secure_password@db:5432/libris_core
      - REDIS_URL=redis://redis:6379/0

  celery:
    build: .
    command: celery -A libris_core worker -l info
    volumes:
      - .:/app
    depends_on:
      - db
      - redis

  celery-beat:
    build: .
    command: celery -A libris_core beat -l info
    volumes:
      - .:/app
    depends_on:
      - db
      - redis

volumes:
  postgres_data:
  static_volume:
  media_volume:
```

### Environment Variables

```bash
# .env
DEBUG=False
SECRET_KEY=your-secret-key-here
DATABASE_URL=postgresql://user:password@localhost:5432/libris_core
REDIS_URL=redis://localhost:6379/0
ALLOWED_HOSTS=localhost,127.0.0.1,yourdomain.com

# Email Configuration
EMAIL_BACKEND=django.core.mail.backends.smtp.EmailBackend
EMAIL_HOST=smtp.gmail.com
EMAIL_PORT=587
EMAIL_USE_TLS=True
EMAIL_HOST_USER=your-email@gmail.com
EMAIL_HOST_PASSWORD=your-app-password
```

---

## Conclusion

This documentation provides a comprehensive overview of the Libris Core Library Management System, including the current React/TypeScript implementation and a detailed guide for converting to Python/Django with advanced analytics using Pandas.

### Key Takeaways:
- **Modular Architecture**: System is designed with clear separation of concerns
- **Scalable**: Can handle growing user base and book inventory
- **Analytics-Driven**: Comprehensive KPI tracking and reporting
- **Automated**: Background tasks for notifications and fine calculations
- **Responsive**: Works across all device sizes
- **Secure**: MFA, password strength validation, role-based access

### Next Steps:
1. Set up Python/Django environment
2. Implement database models
3. Create API endpoints
4. Integrate Pandas for analytics
5. Set up Celery for background tasks
6. Deploy to production environment

For questions or support, contact the development team.

---

**Version**: 1.0.0  
**Last Updated**: December 6, 2025  
**Author**: Libris Core Development Team
