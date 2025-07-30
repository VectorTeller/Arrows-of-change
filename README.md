# Arrows of Change

## National Dynamics in Development, Freedom, Political Integrity, and Digital Inclusion (2013–2023)

This repository contains the complete workflow for an analysis of national development trends over a decade. The project progresses from raw data collection and cleaning to advanced statistical analysis, the creation of a static infographics, and finally, the deployment of a fully interactive web application built with R Shiny.

---

## Project Workflow & Methodology

This project was conducted in three main phases, each building upon the last.

### Phase 1: Data Preparation & Integration

The foundation of this analysis is a composite dataset built from four distinct sources. The goal was to create a clean, reliable dataset for robust time-series analysis.

*   **Data Sources:**
    *   **Human Development (HDI):** United Nations Development Programme (UNDP)
    *   **Political Integrity (CPI):** Transparency International's Corruption Perception Index
    *   **Freedom Scores (Political Rights & Civil Liberties):** Freedom House's "Freedom in the World" report
    *   **Digital Inclusion (Internet Access):** The World Bank's World Development Indicators

*   **Data Preparation Steps:**
    1.  **Load and Filter Data:** Each dataset was loaded into R and filtered to the **2013-2023** period.
    2.  **Standardize Country Names:** A custom R function was developed to standardize country names across all datasets. This function used a combination of manual mapping and string detection to **recode** different naming conventions to a single, consistent identifier for each nation, ensuring that each country could be **equally represented**.
    3.  **Merge with Left Joins:** The standardized datasets were sequentially merged into a master dataframe using the `left_join` operation from `dplyr`, matching observations by country and year.
    4.  **Ensure Complete Coverage:** The merged data was then filtered to include **only countries with complete data coverage** for all key indicators across all 11 years. This step creates a balanced panel, which is crucial for accurate longitudinal analysis.
    5.  **Finalize Dataset:** The final, analysis-ready dataset (`combined_dataset.rds`) was saved to serve as the single source for all subsequent work.

### Phase 2: Analysis & Infographic Design

This phase focused on uncovering the underlying patterns in the data and creating high-impact static visualizations suitable for reports and presentations.

*   **Methodology: Principal Component Analysis (PCA)**
    *   To understand the complex relationships between the four correlated indicators, PCA was applied. This statistical technique reduces the dimensionality of the data, summarizing the four variables into two new, synthetic axes (Principal Components) that collectively explain over 90% of the original variance.
    *   **PC1 (Horizontal Axis):** Was interpreted as an "Overall Development & Openness" index. A high score indicates high human development, low corruption, and high freedom.
    *   **PC2 (Vertical Axis):** Was interpreted as a "Developmental Emphasis" index, contrasting institutional strength with economic/technological focus.

*   **Infographic Creation with `ggplot2`:**
    *   **Main PCA Plot:** The core visualization is a highly customized scatter plot that maps each country's developmental trajectory from 2013 to 2023 as an arrow. A custom bivariate color scale was designed for the background to visually define the four quadrants of the PCA space, with each quadrant annotated with a descriptive title.
    *   **Gauge Plots:** Four circular gauge plots were created to visualize the global shift in the distribution of countries across different development categories between 2013 and 2023.
    *   **Trend Cards:** Small, focused "trend cards" were designed to summarize the decade-long performance of the most dynamic countries identified in the analysis.
    *   All visualizations were created using R's `ggplot2` package and its ecosystem, with final outputs saved as high-resolution PNG and editable SVG files for maximum flexibility.

**[Link to the Final Infographic PDF](path/to/your/infographic.pdf)**

### Phase 3: Interactive Application Development & Deployment

The final phase transformed the static analysis into a dynamic, user-driven tool using R Shiny, making the complex data accessible to a wider audience.

*   **How the Shiny App is Built (The Three-File Structure):**
    *   A Shiny app is best organized into three separate files. This structure separates the app's core functions, making it efficient and easy to manage.
        *   **`global.R` (The Brains):** This script runs only **once** when the app starts. It loads all necessary libraries and performs all the heavy data preparation and PCA calculations. This makes the app fast for the user, as the complex work is done upfront.
        *   **`ui.R` (The Face):** This script defines the User Interface—the layout, sidebar, tabs, buttons, and titles. It controls what the user sees and interacts with.
        *   **`server.R` (The Engine):** This script contains the instructions to build the plots and tables. It runs *reactively*, meaning it listens for user input (like selecting a new country) and instantly redraws the outputs based on that input.

*   **Deployment: From the Cloud to the Web**
    *   To ensure a stable and reproducible development environment, this project was developed in **Posit Cloud**. This cloud-based version of RStudio avoids issues related to local machine configurations (like operating system differences).
    *   To make the app publicly available, the Posit Cloud project was **connected to a `shinyapps.io` account**. The `rsconnect` R package was used to bundle the application files (`global.R`, `ui.R`, `server.R`, and the `data` folder) and deploy them to the `shinyapps.io` hosting service, which generated the permanent public web link.


---




### 🚀 Live Demonstration


Try the interactive Shiny app here:  
👉 **[Click here](https://vectorvoyager.shinyapps.io/arrows_of_change/)**

