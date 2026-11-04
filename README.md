# Recipe and Meal Planning Management System

## Project Overview
Many people keep recipes in cookbooks, websites, social media posts, and personal notes, which makes them hard to organize, search, and reuse. This database stores recipes, ingredients, cooking steps, categories, dietary information, and favorites in one structured place. Users can search by recipe name, ingredient, category, or dietary preference.

## Project Purpose
The database was created to reduce the time spent searching for recipes and deciding what to cook, and to keep recipe information consistent and easy to update. It benefits home cooks, students, busy individuals, families who share recipes, people with dietary restrictions or allergies, and chefs. System administrators can manage user accounts and recipe categories.

## Technologies Used
- **DBMS:** MySQL 8
- **Design tool:** MySQL Workbench (running scripts and importing data)
- **Data:** Excel (.xlsx) and CSV sample data
- **Version control:** Git and GitHub

## Database Features
- Recipes with prep time, cook time, dietary type (vegetarian or non-vegetarian), and allergen warnings
- Ordered cooking steps for each recipe
- Ingredients with quantities and units, searchable across all recipes
- Categories such as Breakfast, Vegan, and Italian, with several categories per recipe
- Favorites, so each user can save recipes
- Households and a shared flag, so family members can view shared recipes
- User roles (cook, family member, admin)
- Primary keys, foreign keys, and junction tables that keep data consistent and reduce duplication (3NF)

## Database Design
link later

The design has nine tables: Household, User, Recipe, Recipe_Step, Ingredient, Category, and three junction tables (Recipe_Ingredient, Recipe_Category, Favorite).

| Relationship | Type | Implemented by |
|---|---|---|
| Household to User | 1:M | User.household_id |
| User to Recipe (owner) | 1:M | Recipe.user_id |
| Recipe to Recipe_Step | 1:M | Recipe_Step.recipe_id |
| Recipe and Ingredient | M:N | Recipe_Ingredient |
| Recipe and Category | M:N | Recipe_Category |
| User and Recipe (favorites) | M:N | Favorite |

**Design decisions:** User has a role column instead of separate Manager and Cooker tables because they share the same fields. Ingredients and steps have their own tables so recipes can be searched by ingredient and each fact is stored once. Quantity sits in Recipe_Ingredient because it describes a recipe and ingredient pair. Shopping lists and content reports were left out to keep the scope focused on recipe storage, searching, sharing, and favorites.

## Project Structure
```
database-design-project/
├── README.md
├── design
    ├── EER_Diagram_RecipeMealPlanning.pdf
    ├── EER_Diagram_RecipeMealPlanning.png
├── sql/
│   └── schema.sql
└── data/
    ├── recipe_meal_planning_sample_data.xlsx
    └── csv/
        ├── Household.csv
        ├── User.csv
        ├── Recipe.csv
        ├── Recipe_Step.csv
        ├── Ingredient.csv
        ├── Recipe_Ingredient.csv
        ├── Category.csv
        ├── Recipe_Category.csv
        └── Favorite.csv
```

## How to Run the SQL Scripts
1. Install MySQL 8 and MySQL Workbench, then connect to your local server.
2. In Workbench, choose **File > Open SQL Script** and open `sql/schema.sql`.
3. Click the lightning bolt (**Execute**). This creates the `recipe_meal_planning` database and all nine tables.
4. Load the sample data from `data/csv/`. In the Navigator, right-click each table and choose **Table Data Import Wizard**. Select the CSV with the same name as the table.
5. Import in this order so foreign keys are satisfied: Household, User, Ingredient, Category, Recipe, Recipe_Step, Recipe_Ingredient, Recipe_Category, Favorite.
6. Check the result with: `SELECT COUNT(*) FROM Recipe;` (expected: 40).

## Team Contributions
| Team member | Responsibilities |
|---|---|
| Huy Nguyen Gia Le | Requirements analysis, table and relationship design, EER diagram, sample data, README |
| Teammate Name | (Add responsibilities, or delete this row if working alone) |
