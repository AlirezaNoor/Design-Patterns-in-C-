# Design Patterns in C#

Design Pattern‌ها راه‌حل‌های اثبات‌شده‌ای برای مشکلات رایج در طراحی نرم‌افزار هستند. در C#، این الگوها به توسعه‌دهندگان کمک می‌کنند تا کدهای قابل‌استفاده، قابل‌درک و قابل‌نگهداری بنویسند. Design Pattern‌ها به سه دسته اصلی تقسیم می‌شوند:

## 1. الگوهای ایجادی (Creational Patterns)

این الگوها به ایجاد اشیا کمک می‌کنند و انعطاف‌پذیری و استفاده مجدد از کد را افزایش می‌دهند.

- **Singleton**: تضمین می‌کند که یک کلاس فقط یک نمونه داشته باشد و یک نقطه دسترسی جهانی به آن نمونه فراهم می‌کند.
- **Factory Method**: یک رابط برای ایجاد اشیا در یک سوپرکلاس فراهم می‌کند، اما اجازه می‌دهند زیرکلاس‌ها نوع شیء ایجاد شده را تغییر دهند.
- **Abstract Factory**: خانواده‌ای از اشیا مرتبط را بدون مشخص کردن کلاس‌های concrete ایجاد می‌کند.
- **Builder**: ساخت یک شیء پیچیده را از نمایش آن جدا می‌کند، بنابراین همان فرآیند ساخت می‌تواند انواع مختلفی از اشیا ایجاد کند.
- **Prototype**: با کپی کردن یک نمونه موجود، اشیا جدید ایجاد می‌کند.

## 2. الگوهای ساختاری (Structural Patterns)

این الگوها به ترکیب کلاس‌ها و اشیا در ساختارهای بزرگ‌تر کمک می‌کنند.

- **Adapter**: اینترفیس یک کلاس را به اینترفیس دیگری تبدیل می‌کند که کلاینت انتظار دارد.
- **Bridge**: یک انتزاع را از اجرای آن جدا می‌کند، بنابراین هر دو می‌توانند به طور مستقل تغییر کنند.
- **Composite**: اشیا را در ساختارهای درختی ترکیب می‌کند تا بتوانند به صورت بخش‌های جداگانه یا کل مجموعه رفتار کنند.
- **Decorator**: رفتار یک شیء را به صورت دینامیک و بدون تغییر در کد آن، گسترش می‌دهد.
- **Facade**: یک رابط ساده‌شده به یک سیستم پیچیده فراهم می‌کند.
- **Flyweight**: با اشتراک‌گذاری بخش‌هایی از حالت بین اشیا، استفاده از حافظه را بهینه می‌کند.
- **Proxy**: یک جایگزین یا نگهدارنده برای یک شیء دیگر فراهم می‌کند تا دسترسی به آن را کنترل کند.

## 3. الگوهای رفتاری (Behavioral Patterns)

این الگوها به ارتباط و توزیع مسئولیت‌ها بین اشیا کمک می‌کنند.

- **Chain of Responsibility**: درخواست‌ها را از طریق زنجیره‌ای از handlers عبور می‌دهد تا زمانی که یکی از آنها درخواست را پردازش کند.
- **Command**: درخواست‌ها را به عنوان اشیا کپسوله می‌کند، بنابراین می‌توان آنها را پارامتریزه کرد و در صف قرار داد.
- **Iterator**: دسترسی به عناصر یک مجموعه را بدون افشای ساختار داخلی آن فراهم می‌کند.
- **Mediator**: ارتباط بین اشیا را با معرفی یک mediator ساده‌تر می‌کند.
- **Memento**: حالت داخلی یک شیء را بدون نقض کپسوله‌سازی ذخیره می‌کند تا بتوان آن را بعداً بازیابی کرد.
- **Observer**: وابستگی یک به چند بین اشیا را تعریف می‌کند، بنابراین وقتی یک شیء تغییر می‌کند، همه وابسته‌های آن مطلع می‌شوند.
- **State**: رفتار یک شیء را بر اساس حالت داخلی آن تغییر می‌دهد.
- **Strategy**: خانواده‌ای از الگوریتم‌ها را تعریف می‌کند، آنها را قابل تعویض می‌کند و اجازه می‌دهد الگوریتم مستقل از کلاینت استفاده شود.
- **Template Method**: الگوریتم را در یک متد تعریف می‌کند، اما اجازه می‌دهد برخی مراحل به زیرکلاس‌ها واگذار شوند.
- **Visitor**: عملیات جدیدی را روی اشیا بدون تغییر در ساختار آنها اضافه می‌کند.

این الگوها به توسعه‌دهندگان C# کمک می‌کنند تا کدهای با کیفیت‌تر و قابل‌نگهداری‌تری بنویسند. هر الگو برای حل یک مشکل خاص طراحی شده است و انتخاب الگوی مناسب بستگی به نیازهای پروژه دارد.
 # Singleton Pattern در C#

Singleton یک الگوی طراحی است که تضمین می‌کند تنها یک نمونه (instance) از یک کلاس وجود داشته باشد و به آن دسترسی جهانی (global access) وجود داشته باشد. این الگو معمولاً در مواردی استفاده می‌شود که شما فقط به یک نمونه از کلاس نیاز دارید، مانند مدیریت اتصال به دیتابیس یا لاگینگ (logging).

## مثال واقعی: Logger (سیستم ثبت رویدادها)

```csharp
public sealed class Logger
{
    // تنها نمونه از کلاس Logger
    private static readonly Logger _instance = new Logger();

    // مسیر فایل لاگ
    private readonly string _logFilePath = "log.txt";

    // سازنده خصوصی برای جلوگیری از ایجاد نمونه‌های جدید
    private Logger()
    {
        // ایجاد فایل لاگ اگر وجود نداشته باشد
        if (!File.Exists(_logFilePath))
        {
            File.Create(_logFilePath).Close();
        }
    }

    // متد برای دسترسی به نمونه Singleton
    public static Logger GetInstance()
    {
        return _instance;
    }

    // متد برای نوشتن لاگ
    public void Log(string message)
    {
        string logMessage = $"{DateTime.Now}: {message}";
        File.AppendAllText(_logFilePath, logMessage + Environment.NewLine);
    }
}

```
## استفاده از Singleton در برنامه
``` csharp
class Program
{
    static void Main(string[] args)
    {
        // دریافت نمونه Singleton
        Logger logger = Logger.GetInstance();

        // نوشتن لاگ
        logger.Log("Application started.");
        logger.Log("Performing some operations...");
        logger.Log("Application ended.");

        // بررسی اینکه فقط یک نمونه وجود دارد
        Logger anotherLogger = Logger.GetInstance();
        Console.WriteLine($"Are both instances the same? {logger == anotherLogger}"); // true
    }
}
```

# Factory Method Pattern Example - Payment System

این پروژه یک مثال عملی از الگوی طراحی **Factory Method** را نشان می‌دهد که در آن یک سیستم پرداخت با استفاده از این الگو پیاده‌سازی شده است.

## الگوی Factory Method

الگوی **Factory Method** یک الگوی طراحی ایجادی (Creational Pattern) است که به شما امکان می‌دهد اشیا را بدون مشخص کردن دقیق کلاس‌هایشان ایجاد کنید. این الگو با تعریف یک متد برای ایجاد اشیا، مسئولیت ایجاد شیء را به زیرکلاس‌ها واگذار می‌کند. این کار باعث می‌شود کد شما انعطاف‌پذیرتر و قابل توسعه‌تر شود.

## ساختار پروژه

در این پروژه، یک سیستم پرداخت ساده پیاده‌سازی شده است که از الگوی Factory Method برای ایجاد روش‌های پرداخت مختلف استفاده می‌کند.

### کلاس‌ها و اینترفیس‌ها

1. **اینترفیس `IPaymentMethod`**:
   - این اینترفیس یک متد به نام `ProcessPayment` دارد که برای پردازش پرداخت استفاده می‌شود.

   ```csharp
   public interface IPaymentMethod
   {
       void ProcessPayment(double amount);
   }
   ```

   کلاس‌های پیاده‌سازی IPaymentMethod:

CreditCardPayment: برای پردازش پرداخت با کارت اعتباری.

PayPalPayment: برای پردازش پرداخت با PayPal.

BankTransferPayment: برای پردازش پرداخت با انتقال بانکی.

``` csharp
public class CreditCardPayment : IPaymentMethod
{
    public void ProcessPayment(double amount)
    {
        Console.WriteLine($"Processing credit card payment of ${amount}");
    }
}

public class PayPalPayment : IPaymentMethod
{
    public void ProcessPayment(double amount)
    {
        Console.WriteLine($"Processing PayPal payment of ${amount}");
    }
}

public class BankTransferPayment : IPaymentMethod
{
    public void ProcessPayment(double amount)
    {
        Console.WriteLine($"Processing bank transfer payment of ${amount}");
    }
}

```

## کلاس PaymentProcessor (Creator):

این کلاس abstract یک Factory Method به نام CreatePaymentMethod تعریف می‌کند.

همچنین یک متد ProcessOrder دارد که از Factory Method برای ایجاد شیء پرداخت و پردازش آن استفاده می‌کند.
``` csharp
public abstract class PaymentProcessor
{
    public abstract IPaymentMethod CreatePaymentMethod();

    public void ProcessOrder(double amount)
    {
        IPaymentMethod paymentMethod = CreatePaymentMethod();
        paymentMethod.ProcessPayment(amount);
    }
}
```


## کلاس‌های Concrete Creator:

``` csharp
CreditCardProcessor: برای ایجاد پرداخت با کارت اعتباری.

PayPalProcessor: برای ایجاد پرداخت با PayPal.

BankTransferProcessor: برای ایجاد پرداخت با انتقال بانکی.


public class CreditCardProcessor : PaymentProcessor
{
    public override IPaymentMethod CreatePaymentMethod()
    {
        return new CreditCardPayment();
    }
}

public class PayPalProcessor : PaymentProcessor
{
    public override IPaymentMethod CreatePaymentMethod()
    {
        return new PayPalPayment();
    }
}

public class BankTransferProcessor : PaymentProcessor
{
    public override IPaymentMethod CreatePaymentMethod()
    {
        return new BankTransferPayment();
    }
}
```

## نحوه اجرای برنامه
برنامه اصلی (Program.cs) از کلاس‌های Concrete Creator برای پردازش پرداخت‌های مختلف استفاده می‌کند.
``` csharp

class Program
{
    static void Main(string[] args)
    {
        PaymentProcessor processor;

        // پرداخت با کارت اعتباری
        processor = new CreditCardProcessor();
        processor.ProcessOrder(100.50);

        // پرداخت با PayPal
        processor = new PayPalProcessor();
        processor.ProcessOrder(200.75);

        // پرداخت با انتقال بانکی
        processor = new BankTransferProcessor();
        processor.ProcessOrder(300.25);
    }
}

```

## خروجی برنامه
با اجرای برنامه، خروجی زیر نمایش داده می‌شود:

 ``` csharp
Processing credit card payment of $100.5
Processing PayPal payment of $200.75
Processing bank transfer payment of $300.25

```


 # دیزاین پترن Builder
دیزاین پترن Builder یکی از الگوهای ایجادی (Creational) است که برای ساخت اشیای پیچیده با استفاده از یک رویکرد گام‌به‌گام استفاده می‌شود. این الگو به ما کمک می‌کند که فرآیند ایجاد یک شیء را از نمایش نهایی آن جدا کنیم، به‌طوری که همان فرآیند ساخت بتواند نمایش‌های مختلفی از آن شیء را تولید کند.

## ساختار الگوی Builder
الگوی Builder از چهار بخش اصلی تشکیل شده است:

- Builder (سازنده‌ی انتزاعی): اینترفیس یا کلاس انتزاعی که مراحل ساخت محصول را مشخص می‌کند.

- ConcreteBuilder (سازنده‌ی مشخص): پیاده‌سازی کلاس Builder که مراحل ساخت محصول را پیاده‌سازی می‌کند.

- Product (محصول نهایی): کلاس شیء پیچیده‌ای که ساخته می‌شود.

- Director (کارگردان): کلاس مسئول مدیریت ترتیب اجرای مراحل ساخت.

## مثال عملی در سی‌شارپ
کلاس Product (محصول نهایی)

``` csharp
public class Burger
{
    public string Bread { get; set; }
    public string Meat { get; set; }
    public bool HasCheese { get; set; }
    public bool HasLettuce { get; set; }

    public void ShowInfo()
    {
        Console.WriteLine($"Burger with {Bread} bread, {Meat} meat, " +
                          $"{(HasCheese ? "with Cheese" : "without Cheese")}, " +
                          $"{(HasLettuce ? "with Lettuce" : "without Lettuce")}");
    }
}
```
## اینترفیس Builder (سازنده‌ی همبرگر)
``` csharp
public interface IBurgerBuilder
{
    void SetBread(string bread);
    void SetMeat(string meat);
    void AddCheese();
    void AddLettuce();
    Burger GetBurger();
}
```

## پیاده‌سازی Concrete Builder (سازنده‌ی مشخص)

``` csharp
public class BurgerBuilder : IBurgerBuilder
{
    private Burger _burger = new Burger();

    public void SetBread(string bread)
    {
        _burger.Bread = bread;
    }

    public void SetMeat(string meat)
    {
        _burger.Meat = meat;
    }

    public void AddCheese()
    {
        _burger.HasCheese = true;
    }

    public void AddLettuce()
    {
        _burger.HasLettuce = true;
    }

    public Burger GetBurger()
    {
        return _burger;
    }
}

```

## کلاس Director (مدیریت ساخت)
``` csharp
public class BurgerDirector
{
    private IBurgerBuilder _builder;

    public BurgerDirector(IBurgerBuilder builder)
    {
        _builder = builder;
    }

    public void MakeClassicBurger()
    {
        _builder.SetBread("Sesame");
        _builder.SetMeat("Beef");
        _builder.AddCheese();
        _builder.AddLettuce();
    }

    public void MakeVeganBurger()
    {
        _builder.SetBread("Whole Grain");
        _builder.SetMeat("Plant-based");
        _builder.AddLettuce();
    }
}

```

# دیزاین پترن Prototype Design Pattern در سی شارپ


  یکی از الگوهای طراحی ایجادی (Creational) است که به جای ایجاد اشیا از ابتدا، از کپی کردن یک نمونه موجود استفاده می‌کند. این الگو زمانی مفید است که ساخت یک شیء هزینه‌بر یا پیچیده باشد و کپی کردن آن ارزان‌تر تمام شود.
  ## توضیح
  ### مراحل پیاده‌سازی


تعریف یک اینترفیس یا کلاس پایه که دارای متد Clone() باشد.

پیاده‌سازی کلاس‌های ConcretePrototype که متد Clone() را اجرا کنند و یک کپی از شیء خود برگردانند.

استفاده از الگو برای ایجاد نمونه‌های جدید از طریق کلون کردن.

### مثال در سی شارپ




``` csharp
using System;

namespace PrototypePattern
{
    // 1. اینترفیس یا کلاس پایه برای کلون کردن اشیا
    public abstract class Prototype
    {
        public abstract Prototype Clone();
    }

    // 2. پیاده‌سازی کلاس ConcretePrototype
    public class Employee : Prototype
    {
        public string Name { get; set; }
        public string Position { get; set; }
        public int Age { get; set; }

        public Employee(string name, string position, int age)
        {
            Name = name;
            Position = position;
            Age = age;
        }

        // پیاده‌سازی متد Clone
        public override Prototype Clone()
        {
            return (Prototype)this.MemberwiseClone(); // کپی سطحی (Shallow Copy)
        }

        public void ShowInfo()
        {
            Console.WriteLine($"Name: {Name}, Position: {Position}, Age: {Age}");
        }
    }

    class Program
    {
        static void Main(string[] args)
        {
            // ایجاد یک نمونه اولیه
            Employee original = new Employee("Ali", "Developer", 30);
            Console.WriteLine("Original Employee:");
            original.ShowInfo();

            // کلون کردن شیء اولیه
            Employee cloned = (Employee)original.Clone();
            cloned.Name = "Reza"; // تغییر مقدار در نسخه کلون شده
            Console.WriteLine("\nCloned Employee (After Modification):");
            cloned.ShowInfo();

            // بررسی اینکه شیء اصلی تغییری نکرده است
            Console.WriteLine("\nOriginal Employee After Clone:");
            original.ShowInfo();
        }
    }
}
```

## الگوی طراحی Adapter در سی شارپ

الگوی Adapter یکی از الگوهای ساختاری (Structural Design Patterns) است که به عنوان مبدل بین دو رابط ناسازگار عمل می‌کند. این الگو زمانی کاربرد دارد که بخواهیم یک کلاس با یک رابط ناسازگار کار کند، بدون اینکه تغییر مستقیمی در آن ایجاد کنیم.

فرض کنید که یک کلاس داریم که اطلاعات را در فرمت JSON پردازش می‌کند، اما یک کلاس دیگر داریم که فقط با فرمت XML کار می‌کند. ما می‌خواهیم این دو کلاس بدون تغییر کد اصلی با هم تعامل داشته باشند. در اینجا، Adapter مشکل را حل می‌کند.

۱. تعریف کلاس‌های موجود (بدون تغییر در آن‌ها)

 ``` csharp

using System;

// کلاس ناسازگار که خروجی JSON تولید می‌کند
class JsonService
{
    public string GetJsonData()
    {
        return "{ \"name\": \"Ali\", \"age\": 25 }";
    }
}

// کلاس ناسازگاری که فقط با XML کار می‌کند
class XmlProcessor
{
    public void ProcessXml(string xmlData)
    {
        Console.WriteLine("Processing XML Data: " + xmlData);
    }
}
```
۲. ایجاد Adapter برای تبدیل JSON به XML

 ```csharp

using System.Xml.Linq;
using Newtonsoft.Json;
using Newtonsoft.Json.Linq;

// Adapter برای تبدیل JSON به XML
class JsonToXmlAdapter : XmlProcessor
{
    private readonly JsonService _jsonService;

    public JsonToXmlAdapter(JsonService jsonService)
    {
        _jsonService = jsonService;
    }

    public void ProcessJsonAsXml()
    {
        // دریافت داده‌های JSON
        string jsonData = _jsonService.GetJsonData();
        
        // تبدیل JSON به XML
        JObject jsonObject = JObject.Parse(jsonData);
        XElement xmlData = new XElement("Person",
            new XElement("Name", jsonObject["name"]),
            new XElement("Age", jsonObject["age"])
        );

        // ارسال XML به کلاس ناسازگار
        ProcessXml(xmlData.ToString());
    }
}

````


۳. استفاده از Adapter در برنامه
```csharp
class Program
{
    static void Main()
    {
        // نمونه‌ای از کلاس JSON که قصد داریم از آن در سیستم XML استفاده کنیم
        JsonService jsonService = new JsonService();

        // استفاده از Adapter برای تبدیل JSON به XML
        JsonToXmlAdapter adapter = new JsonToXmlAdapter(jsonService);
        adapter.ProcessJsonAsXml();  // پردازش XML از داده‌های JSON
    }
}
````



