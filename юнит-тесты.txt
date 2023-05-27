namespace CalculationsTestProject;
using CalculationsLib;

[TestClass]
public class CalculationsUnitTest
{
    [TestMethod]
    public void AvailablePeriodsTest_GivenValidPeriodsWithShortConsultTime_returnValidResult()
    {
        // Arrange
        TimeSpan[] startTimes = new TimeSpan[]
        {
            TimeSpan.Parse("08:00"),
            TimeSpan.Parse("08:10"),
            TimeSpan.Parse("08:30")
        };
        int[] durations = new int[] { 10, 20, 30 };
        TimeSpan beginWorkingTime = TimeSpan.Parse("08:00");
        TimeSpan endWorkingTime = TimeSpan.Parse("10:00");
        int consultationTime = 10;

        // Act
        string[] expected = new[]
        {
            "09:00:00 - 09:10:00",
            "09:10:00 - 09:20:00",
            "09:20:00 - 09:30:00",
            "09:30:00 - 09:40:00",
            "09:40:00 - 09:50:00",
            "09:50:00 - 10:00:00",
        };
        string[] actual =
            Calculations.AvailablePeriods(startTimes, durations, beginWorkingTime, endWorkingTime, consultationTime);

        // Assert
        CollectionAssert.AreEqual(expected, actual);
    }
    
    [TestMethod]
    public void AvailablePeriodsTest_GivenValidPeriodsWithNoFreeTime_returnEmptyResult()
    {
        // Arrange
        TimeSpan[] startTimes = new TimeSpan[]
        {
            TimeSpan.Parse("08:00"),
            TimeSpan.Parse("08:10"),
            TimeSpan.Parse("08:30")
        };
        int[] durations = new int[] { 10, 20, 30 };
        TimeSpan beginWorkingTime = TimeSpan.Parse("08:00");
        TimeSpan endWorkingTime = TimeSpan.Parse("10:00");
        int consultationTime = 80;

        // Act
        string[] expected = new string[] {};
        string[] actual =
            Calculations.AvailablePeriods(startTimes, durations, beginWorkingTime, endWorkingTime, consultationTime);

        // Assert
        CollectionAssert.AreEqual(expected, actual);
    }
}