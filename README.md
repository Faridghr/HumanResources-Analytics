
# HR Dashboard Project

## Project Objective

This project simulates a real-world HR dashboard designed for effective data analysis and visualization. 
We start by gathering requirements from key stakeholders such as sales managers and HR managers, analyzing the data, and determining the appropriate visualizations.
After understanding the dataset, we proceed with creating a data model in Tableau, followed by building the charts and dashboards.

Visit the [Tableau Dashboard](https://public.tableau.com/views/HRDashboard_17272452495470/HRSummary?:language=en-US&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link) to explore the visualizations and gain insights into human resources data.

## User Story - HR Dashboard

As an HR manager, I require a comprehensive dashboard that provides a holistic view of HR data. This dashboard should include both summary views for high-level insights and detailed employee records for in-depth analysis.

### Summary View

The **Summary View** consists of three main sections: Overview, Demographics, and Income Analysis. Each section provides critical information to help manage and understand workforce dynamics.

#### Overview

The **Overview** section gives an essential snapshot of HR metrics:

1. **Total Hired, Active, and Terminated Employees**
- **Chosen Chart:** Big Ass Numbers (BANs) for the total count of hired, active, and terminated employees.

2. **Employee Hiring and Termination Trends Over the Years**:
- **Chosen Chart:** Line chart to visualize hiring and termination trends over time.

3. **Breakdown of Total Employees by Department and Job Title**: 
- **Chosen Chart:** Bar charts to display the total employees per department and job title.

4. **Employee Comparison Between Headquarters (HQ) and Branches**: 
- **Chosen Chart:** Map visualization with New York as the HQ and other locations categorized as branches.

5. **Distribution of Employees by City and State**: 
- **Chosen Chart:** Enhanced map with city shapes indicating employee distribution by location, with varying size for each city.

#### Demographics

The **Demographics** section provides detailed insights into the workforce composition:

1. **Gender Ratio in the Company**: 
- **Chosen Chart:** Pie chart to visualize the gender ratio.

2. **Distribution of Employees by Age Groups and Education Levels**: 
- **Chosen Chart:** Heatmap to illustrate the correlation between age and education levels.

3. **Age Group Breakdown of Employees**: 
- **Chosen Chart:** Bar chart to show the total number of employees in each age group.

4. **Education Level Breakdown of Employees**: 
- **Chosen Chart:** Bar chart to show the total employees by education level.

5. **Correlation Between Educational Background and Performance Ratings**: 
- **Chosen Chart:** Heatmap to visualize the relationship between education and performance.

#### Income Analysis

The **Income Analysis** section focuses on salary data, exploring compensation patterns:

1. **Salary Comparison Across Education Levels and Genders**: 
- **Chosen Chart:** Barbell chart to compare salaries between genders for different education levels.

2. **Correlation Between Age and Salary Across Departments**: 
- **Chosen Chart:** Scatter plot to display the relationship between age and salary in various departments.

### Employee Records View

The **Employee Records View** provides a comprehensive list of all employees, detailing their personal information, job data, and salary. Users can filter the list based on any column, allowing for customized exploration of employee data.

## Dataset

The dataset used in this HR Dashboard project is generated using the Python `Faker` library. It simulates employee information commonly found in HR systems, such as demographics, job details, salary, performance ratings, and attrition. This dataset provides a rich source of data for analysis and visualization in Tableau.

### Key Fields:

- **Employee ID**: A unique identifier for each employee.
- **Name**: Randomly generated first and last names.
- **Gender**: Assigned randomly, with a 46% probability for ‘Female’ and a 54% probability for ‘Male.’
- **State and City**: Randomly selected from a predefined list.
- **Hire Date**: Randomly generated, with a probability distribution from 2015 to 2024.
- **Department and Job Title**: Assigned with specific probabilities for each department and title.
- **Education Level**: Mapped to job titles and assigned accordingly.
- **Performance Rating**: Randomly chosen based on probabilities for different performance levels.
- **Overtime**: Assigned with a 30% probability for 'Yes.'
- **Salary**: Determined based on department and job title, with a range of salaries.
- **Birth Date**: Generated to ensure consistency with age and hire date.
- **Termination Date**: Assigned to 11.2% of employees, with probabilities ensuring at least a six-month gap between hire and termination dates.

## Calculated Fields

Key calculated fields used in this Tableau dashboard:

1. **Total Hired**: `COUNT([Employee ID])`
2. **Total Terminated**: `COUNT(IF NOT ISNULL([Termination Date]) THEN [Employee ID] END)`
3. **Total Active**: `COUNT(IF ISNULL([Termination Date]) THEN [Employee ID] END)`
4. **Location**: Distinguishes between HQ and branches:
   ```sql
   CASE [State]
       WHEN 'New York' THEN 'HQ'
       ELSE 'Branch'
   END
   ```
5. **Age**: Calculates employee age: `DATEDIFF('year', [Birth Date], TODAY())`
6. **Age Group**: Categorizes employees into age groups:
   ```sql
   IF [Age] < 25 THEN '>25'
   ELSEIF [Age] >= 25 AND [Age] < 35 THEN '25-34'
   ELSEIF [Age] >= 35 AND [Age] < 45 THEN '35-44'
   ELSEIF [Age] >= 45 AND [Age] < 55 THEN '45-54'
   ELSEIF [Age] >= 55 THEN '55+'
   END
   ```

## Screen Shots

![HR Summary](png/Summary.JPG)

![HR Detail](png/Detail.JPG)
