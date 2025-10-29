# did-analysis-toolkit
This toolkit provides a robust, extended Difference-in-Differences (DiD) framework for causal analysis. It features 5-term regression with cluster-robust standard errors and Synthetic Control logic to ensure credible results by rigorously validating the Parallel Trends Assumption before estimating the causal impact ($\text{ATT}$).

**Difference-in-Differences (DiD) Causal Analysis Toolkit**

This Python toolkit contains all necessary functions to perform a robust, extended Difference-in-Differences (DiD) regression analysis on time-series panel data. It is specifically designed to isolate the causal effect of a single intervention (like a product launch or policy change) by controlling for pre-existing trends and using cluster-robust standard errors.

The toolkit was developed to analyze the impact of the New Home Page Launch on user engagement and profitability metrics.

**Key Features and Methodology**

**1. Extended DiD Model:** Implements a 5-term DiD regression that includes Group-Specific Linear Time Trends ($\text{Time}$ and $\text{Time} \times \text{Treated}$). This is crucial for relaxing the strict Parallel Trends Assumption (PTA) and accounting for pre-existing differences in growth/decline rates between the treated and control groups.

**2. Cluster-Robust Standard Errors:** All regressions use $\text{cluster-robust standard errors}$ (clustered by: $\text{'lp category'}$) to correct for autocorrelation inherent in time-series data, ensuring the statistical significance ($P$-values) is reliable.

**3. Assumption-Driven Control Selection:** Includes a function to automatically calculate the $\text{Pre-Period Trend Similarity (Correlation)}$ between the treated group and various control candidates, guiding the user to select the most credible counterfactual for each outcome metric.

**4. Synthetic Control Implementation:** Includes an optimization function to generate a Synthetic Control Group when no single control unit provides an adequate pre-trend match.

**5. Comprehensive Visualizations:** Provides three distinct plotting functions for validation and communication:

- plot_metric_timeline: Shows raw trends for PTA visual validation.

- plot_metric_subplots: Provides a clean, side-by-side view of the paired groups.

- plot_did_summary: Generates the classic four-point causal visual, clearly illustrating the estimated $\text{DID}$ effect ($\text{ATT}$) against the counterfactual.

Function | Purpose
-- | --
clean_landing_page_data | Cleans, aggregates, feature-engineers, and applies a data maturity filter (removes recent, unstable days).
merge_dataframes | Merges LP data with session data and calculates all final ratio metrics (e.g., $\text{roas internal}$, $\text{session 2 search}$).
analyze\_did\_assumptions | Calculates the pre-period correlation between all $\text{DID METRICS}$ and potential control pages to guide control group selection.
run\_did\_regression | Executes the 5-term $\text{OLS}$ regression and returns the $\text{statsmodels}$ results object with cluster-robust errors.
plot\_did\_summary | Visualizes the causal effect ($\text{DID}$ coefficient) as a four-point graph (Control Actual, Treated Actual, Counterfactual).

<h3>Setup and Usage</h3><ol><li><p><strong>Define Configuration:</strong> Update the <code>NEW_HOME_PAGE_DATE</code> variable within the script.</p></li><li><p><strong>Load Data:</strong> Load your raw <math-inline data-math="\text{LP}">$\text{LP}$</math-inline> and <math-inline data-math="\text{Sessions}">$\text{Sessions}$</math-inline> dataframes.</p></li><li><p><strong>Run Pipeline:</strong> Call the cleaning and merging functions to generate the final analytical DataFrame.</p></li><li><p><strong>Analyze &amp; Model:</strong> Use <math-inline data-math="\text{analyze\_did\_assumptions}()">$\text{analyze\_did\_assumptions}()$</math-inline> to select the control group, and then use <math-inline data-math="\text{run\_did\_regression}()">$\text{run\_did\_regression}()$</math-inline> for the final causal estimates.</p></li></ol>
