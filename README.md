Overview
This project transforms a raw, messy e-commerce orders dataset (1,200 records) into a clean, analysis-ready dataset using Python and Pandas. The goal was to identify and resolve missing values, duplicate records, and inconsistent formatting — establishing a reliable foundation before any analysis or modeling work.
Problem
Raw business data is rarely clean. This dataset contained:
Missing values in the CouponCode column (294 records)
Inconsistent date formats
Inconsistent text casing and whitespace across categorical columns
Unrounded numeric/price values
Potential duplicate order records
Approach
Rather than blindly deleting incomplete rows or applying a single fill strategy to everything, each issue was diagnosed individually and treated based on what the missing or inconsistent value actually represented:
Duplicates were identified and removed based on OrderID uniqueness.
Missing CouponCode values were labeled "None" rather than imputed with the most frequent coupon — since a blank coupon field almost certainly means no coupon was used, not that data was lost. Imputing it with a real coupon code would have fabricated information.
Dates were standardized to ISO 8601 format (YYYY-MM-DD) for consistency and easier downstream analysis.
Text fields (Product, ShippingAddress, PaymentMethod, OrderStatus, ReferralSource) were trimmed of whitespace and standardized to Title Case.
Price fields were rounded to 2 decimal places.
Data integrity check: cross-validated Quantity × UnitPrice against TotalPrice to catch potential calculation errors (0 mismatches found).
Verification
Per the project's quality gate, the cleaned dataset was verified to have:
✅ 0% duplicate Order IDs
✅ 0% incorrectly formatted dates
Tech Stack
Python 3
Pandas / NumPy
ReportLab (PDF change log generation)
