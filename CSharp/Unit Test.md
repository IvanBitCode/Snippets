# Unit Test
Create Unit Test in Visual Studio

`Solution > Right click > Add > New Project > Unit Test Project (.Net Framework)`

The naming convention for the unit test project is:

`<SolutionName>.UnitTests`

The naming convention for the test class is:

`<ClassName>Tests`

The naming convention for the test method is: 

`<MethodName>_Scenario_ExpectedBehaviour`

To get the scenario and expected behaviour, we need to consider the execution paths of our method. For example:

```cs
namespace Reviewer.UnitsTests
{
    [TestClass]
    public class AttachmentReviewerTests
    {
        [TestMethod]
        public void Review_ZeroEmbbeddedFiles_ReturnsFalse()
        {
        }
    }
}
```

Inside every test method we have three paths: 
* **Arrange**. Where we initialize our objects we want to test.
* **Act**. Where we call the method we are going to test.
* **Assert**. Where we set the expected result.

Example

```cs
[TestClass]
public class AttachmentReviewerTests
{
    [TestMethod]
    public void Review_ZeroEmbbeddedFiles_ReturnsFalse()
    {
         // Arrage
         var embbededFiles = new string[] { "0 embbeded files" }

         // Act
         (bool success, _) = attachmentReviewer.Review("file1.c", "file2.h", embbededFiles);

         // Assert
         Assert.IsFalse(success);
    }
}
```
