# SOLID Principles in Ruby (for Rails Developers)

This document covers the SOLID design principles tailored for Ruby (and especially Ruby on Rails) developers, with real-world examples and code relevant to service objects, modules, and domain logic.

---

## 1. Single Responsibility Principle (SRP)

### What it is
A class should have one and only one reason to change. It should do one thing and do it well.

### What if not used
Classes become bloated and hard to maintain. A small change in one area can unintentionally break another.

### Advantage
- Easier to maintain and test
- Clear separation of concerns
- Better debugging and reuse

### Code
```ruby
# Bad: User class handles both data and report generation
class User
  def initialize(name)
    @name = name
  end

  def generate_report
    # logic to generate report
  end
end

# Good: Responsibility is separated
class User
  attr_reader :name

  def initialize(name)
    @name = name
  end
end

class ReportGenerator
  def generate(user)
    # generate report for user
  end
end
```

---

## 2. Open/Closed Principle (OCP)

### What it is
Classes should be open for extension, but closed for modification.

### What if not used
Any new change requires altering existing code, increasing the chance of introducing bugs.

### Advantage
- Flexible and extensible code
- Avoids regression when adding new features

### Code
```ruby
# Bad: Modifying for every new notification type
class Notification
  def send(type)
    if type == 'email'
      # send email
    elsif type == 'sms'
      # send sms
    end
  end
end

# Good: Extend behavior using polymorphism
class Notification
  def send
    raise NotImplementedError
  end
end

class EmailNotification < Notification
  def send
    # send email
  end
end

class SMSNotification < Notification
  def send
    # send sms
  end
end
```

---

## 3. Liskov Substitution Principle (LSP)

### What it is
Subclasses should be substitutable for their parent class without changing the program behavior.

### What if not used
Code that works with the parent class might break when using a subclass.

### Advantage
- Safe and reliable inheritance
- Prevents hidden bugs

### Code (Rails-style example)
```ruby
# Bad: PDFExporter doesn't behave like other Exporters
class BaseExporter
  def export(data)
    raise NotImplementedError
  end
end

class CSVExporter < BaseExporter
  def export(data)
    # export to CSV
  end
end

class PDFExporter < BaseExporter
  def export(data)
    raise "PDF export not supported"
  end
end

# Good: Clear interfaces and separation
module Exportable
  def export(data)
    raise NotImplementedError
  end
end

class CSVExporter
  include Exportable

  def export(data)
    # logic to export
  end
end

# Only use exporters that implement Exportable
```

---

## 4. Interface Segregation Principle (ISP)

### What it is
Don’t force a class to implement methods it doesn’t need. Ruby solves this via module mixins.

### What if not used
Classes become bloated with unused or unrelated logic.

### Advantage
- Focused modules and services
- Improved clarity and testability

### Code (Rails real-world example)
```ruby
# Bad: One big Notifier module
module Notifier
  def send_email(user); end
  def send_sms(user); end
  def send_push_notification(user); end
end

class EmailService
  include Notifier

  def send_email(user)
    # OK
  end

  def send_sms(user)
    raise NotImplementedError
  end
end

# Good: Split per responsibility
module EmailNotifiable
  def send_email(user); end
end

module SMSNotifiable
  def send_sms(user); end
end

class EmailService
  include EmailNotifiable

  def send_email(user)
    # Only email
  end
end
```

---

## 5. Dependency Inversion Principle (DIP)

### What it is
High-level classes should not depend on low-level classes. Both should depend on abstractions.

### What if not used
Code becomes tightly coupled and hard to test or replace.

### Advantage
- Decouples logic and infrastructure
- Better for testing and swapping dependencies

### Code
```ruby
# Bad: UserNotifier depends directly on EmailService
class EmailService
  def send_email
    # logic
  end
end

class UserNotifier
  def initialize
    @service = EmailService.new
  end

  def notify
    @service.send_email
  end
end

# Good: Inject dependency
class UserNotifier
  def initialize(messenger)
    @messenger = messenger
  end

  def notify
    @messenger.send
  end
end

class EmailService
  def send
    # send email
  end
end

notifier = UserNotifier.new(EmailService.new)
notifier.notify
```

---

Feel free to adapt these principles to your context and refactor gradually.


