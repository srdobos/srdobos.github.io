If you have multiple terms that must be true in order to perform some operation, give the terms names and store their truth value.

```csharp
// instead of a complex mash of operators

if (data != null && data.IsValid() && operator != null && operator.CanOperateOn(data) &&
    dataPrinter != null && dataPrinter.IsInitialized() && 
    (dataPrinter is IDataPrinter<SomeSpecificType> || dataPrinter.CanPrintData(data)))
{
    // do stuff
}


// do it with explicit naming

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

Yes, it is more verbose to use explicit names. However, this is a good thing in the case of complex conditionals. An engineer who is unfamiliar with the above block of code will not have to manually parse the if statement to make sense of it. You've done all the work for him and assigned labels to each part. You've clearly outlined what is required for the data to be valid, what is required for the operator to be valid, what is required for the data to be printed, and (most important) you've made it obvious what high level parts need to be true for the operation to be performed.

Breaking that if statement into simple named booleans allows people reading through the code to save some brain processing power for what really matters, understanding it as a whole.