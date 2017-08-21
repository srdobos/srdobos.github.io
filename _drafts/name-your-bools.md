---
layout: post
title: Name your bools
---

Often, when digging into a library or reading unfamiliar code, I come across conditional statements that quite verbose. They contain several logical terms joined together with && or ||. If I can avoid having to understand the conditional, I will. However, more often than not, the understanding logic expressed in that conditional statement is unavoidable. So I must mentally break it apart into digestible chunks and parse it to see what is happening. This interrupts the flow of understanding the greater system.

Conditional bloat is a symptom of overall code bloat. A bloated conditional probably started out simple, with only one or two terms. More and more terms were added as the project grew. No one took the time to refactor it for clarity.

###Name your bools

When there are multiple terms that must be true in order to perform some operation, provide names for each logical set of terms and store their truth value.

```csharp
// instead of a complex mash of operators

if (data != null && data.IsValid() && operator != null && operator.CanOperateOn(data) &&
    dataPrinter != null && dataPrinter.IsInitialized() && 
    (dataPrinter is IDataPrinter<SomeSpecificType> || dataPrinter.CanPrintData(data)))
{
    // do stuff
}


// use explicit names to provide context and clarity

bool dataIsValid = data != null && data.IsValid();

bool operatorIsValid = operator != null && operator.CanOperateOn(data);

bool dataPrinterIsReady = dataPrinter != null && dataPrinter.IsInitialized();
bool dataCanBePrinted = dataPrinterIsReady && (dataPrinter is IDataPrinter<SomeSpecificType> || dataPrinter.CanPrintData(data));

bool canPerformOperation = dataIsValid && operatorIsValid && dataCanBePrinted;

if (canPerformOperation)
{
    // do stuff
}
```

While it is more verbose to use explicit names, this is a good thing in the case of complex conditionals. An engineer who is unfamiliar with the above block of code will not have to mentally parse the if statement to make sense of it. Here, we have done all the work for him by assigning labels to each part. We have clearly outlined what is required for the data to be valid, what is required for the operator to be valid, what is required for the data to be printed, and (most important) we've made it obvious what high level parts need to be true for the operation to be performed.

Breaking that if statement into simple named booleans allows people who are reading through the code to save some brain power for what really matters, understanding it as a whole.