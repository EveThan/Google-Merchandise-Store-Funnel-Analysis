# Google Merchandise Store — E-commerce Data Conversion Funnel Dashboard

<p align="center"> <img height="600" alt="image" src="https://github.com/user-attachments/assets/b29f4630-9ac6-4899-8129-be01b111a49e" /> </p>


## 1. Project Goal
The goal of this project is to build an easy-to-use dashboard that helps stakeholders quickly understand
1. The overall closed conversion funnel performance
2. How conversion rates differ when segmented by device type, traffic source, geography, and item category

This dashboard helps us pinpoint where users drop off most and identify areas for optimization.

## 2. Data
The dataset used is the [ga4_obfuscated_sample_ecommerce dataset](https://console.cloud.google.com/bigquery?p=bigquery-public-data&d=ga4_obfuscated_sample_ecommerce&t=events_20210131&page=table) available through BigQuery Public Datasets. It contains a sample of BigQuery event export data for three months from 2020-11-01 to 2021-01-31.

## 3. Link to Dashboard and Google Colab
The interactive dashboard can be accessed on [Looker Studio](https://lookerstudio.google.com/reporting/4eb3dffd-6e26-4f4d-8046-82e60102948e), while all SQL used for data processing and complete analysis notes can be found on [Google Colab](https://colab.research.google.com/drive/1iEq6xPdefjna970kkfhkkkT9nhhARYfN#scrollTo=laItJf6f5QAS).

## 4. Conversion Funnel Setup
The conversion funnel consists of the following GA4 events \
session_start → view_item → add_to_cart → begin_checkout → add_shipping_info → add_payment_info → purchase.

Details behind the selection of these events as conversion funnel stages can be found on [Google Colab](https://colab.research.google.com/drive/1iEq6xPdefjna970kkfhkkkT9nhhARYfN#scrollTo=BDjTuA4GL0f3).

This analysis uses a user-based conversion funnel, which means that each user is counted only once. This differs from session-based funnels where a user can be counted multiple times across different sessions.

Additionally, a closed funnel approach is implemented, which means that only users who proceed through the funnel stages in the order above (session_start → view_item → add_to_cart → ...) are included, although they may drop off at any step. Users who skip stages or complete them out of order are not included in the conversion funnel.

In the interactive dashboard, the conversion funnel is also anchored on each user's session_start_date. This means that users are included in the conversion funnel if their session_start_date falls within the selected date range. All subsequent funnel events (e.g., view_item, add_to_cart, purchase) are attributed to that same session_start_date and are counted in the conversion funnel even if they occurred outside the selected date range. This ensures a more complete view of user progression through the funnel after their first visit which happened within the selected date range.

## 5. Conversion Funnel Insights Summary
### 5.1. Overall Conversion Funnel ([view analysis summary on Google Colab](https://colab.research.google.com/drive/1iEq6xPdefjna970kkfhkkkT9nhhARYfN#scrollTo=6haBQ7AgKX8i))
1. 80.04% drop-off from session_start to view_item
   - May be due to low-intent user traffic or unclear website navigation. Potential solution includes improving ad targeting and landing page UI and UX.

2. 84.80% drop-off from view_item to add_to_cart
   - May be due to high prices, low or unavailable stock, or insufficient product information. Potential solution includes improving product detail pages and ensuring ad copies accurately reflect the products.

3. 86.09% drop-off from add_to_cart to begin_checkout
   - May be due to the pop-up window requesting account creation and a lack of urgency (e.g., no low stock indicators or limited-time offers). Potential solutions include removing the barrier of account creation and introducing urgency nudges such as time-sensitive deals.

4. 37.98% drop-off from add_shipping_info to add_payment_info
   - May be due to high shipping costs or long delivery times. Potential solutions include offering free shipping on qualifying orders and improving logistics to ensure faster delivery.

### 5.2. 📱 Segmentation by Device Type ([view analysis summary on Google Colab](https://colab.research.google.com/drive/1iEq6xPdefjna970kkfhkkkT9nhhARYfN#scrollTo=R0tX7hvJKnvH))
Tablet users had ~3% lower conversion rates at payment and purchase stages. However, the conversion rate differences are not drastic, implying that user experience appears to be consistent across device types.

### 5.3. 🌍 Segmentation by Country and Continent ([view analysis summary on Google Colab](https://colab.research.google.com/drive/1iEq6xPdefjna970kkfhkkkT9nhhARYfN#scrollTo=uQ19ICSsKvD7))
Overall, there are no major differences in stage-to-stage conversion rates across countries or continents.

### 5.4.🚦 Segmentation by Traffic Source ([view analysis summary on Google Colab](https://colab.research.google.com/drive/1iEq6xPdefjna970kkfhkkkT9nhhARYfN#scrollTo=lo6tVZ6Xl7A3))
Referral had ~14% lower conversion rate at the purchase stage compared to cpc (advertisement) and organic. May be worthwhile to investigate the quality of referral sources and potential referral promo code issues.

### 5.5. 👕 Segmentation by Item Category ([view analysis summary on Google Colab](https://colab.research.google.com/drive/1iEq6xPdefjna970kkfhkkkT9nhhARYfN#scrollTo=xHOundOvxrL4))
Collections consistently performed well across all stages. Apparel and Lifestyle categories had lower purchase rates despite getting the most traffic. May be worthwhile to address possible friction in their checkout process. Shop by Brand and New had the lowest early-stage conversion rates.

## 6. Additional Analysis
### 6.1. Returning Behavior ([view analysis summary on Google Colab](https://colab.research.google.com/drive/1iEq6xPdefjna970kkfhkkkT9nhhARYfN#scrollTo=bU7sG12bd6sq))
Most users return within 7 days of their last visit (72–76%). Purchasers are more likely than visitors to return after 8–30 days.

### 6.2. Average Time to Purchase
On average, it takes 5.3 days from a user’s first visit to their first purchase. Changing the date range in [the interactive dashboard](https://lookerstudio.google.com/reporting/4eb3dffd-6e26-4f4d-8046-82e60102948e) shows different values for Average Days to Purchase.
