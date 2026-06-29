# 🚀 Clean Architecture CQRS Template (.NET 10)

![.NET 10](https://img.shields.io/badge/.NET-10.0-purple?style=for-the-badge&logo=dotnet)
![Clean Architecture](https://img.shields.io/badge/Clean-Architecture-success?style=for-the-badge)
![CQRS](https://img.shields.io/badge/Pattern-CQRS-blue?style=for-the-badge)
![MediatR](https://img.shields.io/badge/Library-MediatR-orange?style=for-the-badge)

A Production-Ready, Enterprise-Grade Boilerplate for building scalable .NET 10 Web APIs using Clean Architecture and CQRS principles. 

هذا المشروع عبارة عن قالب أساسي (Template) جاهز للاستخدام لبناء أنظمة برمجية ضخمة (Enterprise Applications) متوافقة مع أحدث معايير هندسة البرمجيات باستخدام **.NET 10**.

---

## ✨ Features (المميزات الأساسية)

- **[x] .NET 10:** Built with the latest .NET framework for maximum performance.
- **[x] Clean Architecture:** Strictly follows Domain-Centric design (Domain, Application, Infrastructure, API).
- **[x] CQRS Pattern:** Complete separation of Read (Queries) and Write (Commands) operations using `MediatR`.
- **[x] Cross-Cutting Validation:** Centralized validation pipeline using `FluentValidation` and `MediatR Pipeline Behaviors` (No validation logic inside controllers).
- **[x] Generic Repository Pattern:** A clean, reusable, and extendable generic repository implementation (`IRepository<T>`).
- **[x] Advanced Pagination:** Built-in `PagedResult<T>` for handling large datasets efficiently.
- **[x] Global Exception Handling:** Utilizes .NET's modern `IExceptionHandler` to catch and standardize all exceptions into `ProblemDetails` format effortlessly.
- **[x] Thin Controllers:** API endpoints contain zero business logic, acting purely as dispatchers.

---

## 🏗️ Architecture Layers (هيكل المشروع)

The solution is divided into 4 main layers strictly following the Dependency Rule:

1. **`Domain`**: 
   The core of the system. Contains Entities, Enums, and Value Objects. *Has no dependencies on any other project.*
   
2. **`Application`**: 
   The brain of the system. Contains Business Logic, CQRS (Commands/Queries), Interfaces (`IRepository`), DTOs, and the Validation Pipeline. *Depends only on the Domain layer.*
   
3. **`Infrastructure`**: 
   The muscle. Handles external concerns like Database access (`AppDbContext`), EF Core configurations, and the concrete implementation of repositories (`Repository<T>`). *Depends on the Application layer.*
   
4. **`API` (Presentation)**: 
   The entry point. Contains Controllers, Global Exception Middleware (`GlobalException`), and Dependency Injection configurations. *Depends on Application and Infrastructure layers.*

---

## 🛠️ Tech Stack & Libraries (التقنيات المستخدمة)

- **Framework:** .NET 10.0
- **Database Access:** Entity Framework Core (SQL Server)
- **Mediator Pattern:** MediatR (`MediatR`)
- **Validation:** FluentValidation (`FluentValidation.DependencyInjectionExtensions`)
- **API Documentation:** OpenAPI / Swagger (Native .NET 10 approach)

---

## 🧠 Highlighted Implementations (لماذا هذا القالب؟)

### 1. Smart Validation Pipeline
بدلاً من تكرار كود الـ Validation في كل Controller، تم بناء `ValidationBehavior` يعترض أي طلب (Request) قبل وصوله للـ Handler، ويقوم بتشغيل شروط `FluentValidation` تلقائياً، ويرمي خطأ مجمع إذا كانت البيانات غير صالحة.

### 2. Modern Exception Handling
لا يوجد `try-catch` في المشروع! تم استخدام `IExceptionHandler` المركزي لاصطياد الأخطاء (مثل أخطاء הـ Validation أو הـ NotFound) وتحويلها تلقائياً إلى استجابة قياسية (Standardized Problem Details JSON).

### 3. Generic Repository with Pagination
يحتوي المشروع على مستودع عام يدعم الـ Filtering، والـ Includes، ودالة مخصصة `GetAll` تُرجع `PagedResult<T>` لضمان عدم تحميل الذاكرة (RAM) ببيانات غير ضرورية.

---

## 🚀 Getting Started (كيفية التشغيل)

### Prerequisites
- [.NET 10 SDK](https://dotnet.microsoft.com/download/dotnet/10.0) installed on your machine.
- SQL Server (LocalDB or Docker instance).
- Visual Studio 2022 (latest preview for .NET 10 support) or Rider/VS Code.

### Steps
1. **Clone the repository:**
   ```bash
   git clone [https://github.com/YourUsername/YourRepositoryName.git](https://github.com/YourUsername/YourRepositoryName.git)
   Update Connection String:
Navigate to GitHub_CleanArch/appsettings.json and update the DefaultConnection to match your SQL Server instance.

Apply Migrations:
Open the Package Manager Console (PMC) or Terminal and run:

Bash
dotnet ef database update --project Infrastructure --startup-project GitHub_CleanArch
Run the API:
Hit F5 in Visual Studio or run:

Bash
dotnet run --project GitHub_CleanArch
🤝 Contribution
Feel free to fork this repository, submit pull requests, or open issues to improve this template. Let's build better software together!

Built with ❤️ focusing on Clean Code and Enterprise Standards.
