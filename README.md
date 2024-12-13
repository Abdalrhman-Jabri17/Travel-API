# Laravel Hiring Test

## Project Overview
Create a Laravel APIs application for a travel agency.

### Glossary
- **Travel**: The main unit of the project, containing all necessary information such as the number of days, images, title, etc.  
  Examples:
  - *Japan: Road to Wonder*
  - *Norway: The Land of the Ice*

- **Tour**: A specific date range of a travel with its own price and details.  
  Example:
  - *Japan: Road to Wonder* may have:
    - A tour from **10 to 27 May** at **€1899**.
    - Another tour from **10 to 15 September** at **€669**.

  *At the end, users will book a tour, not a travel.*

---

## Goals
By the end of the project, the application should have:

### Private (Admin) Endpoints:
1. **Create New Users**:
   - Optionally implemented as an Artisan command.
   - Primarily used to generate users for this exercise.
   
2. **Create New Travels**.

3. **Create New Tours for a Travel**.

### Private (Editor) Endpoint:
1. **Update a Travel**.

### Public (No Authentication) Endpoints:
1. **List of Paginated Travels**:
   - Returns only public travels.

2. **List of Paginated Tours by Travel Slug**:
   - Example: `GET /travels/foo-bar/tours`.
   - Supports filtering by:
     - `priceFrom`, `priceTo` (tour price range).
     - `dateFrom` (starting date).
     - `dateTo` (ending date).
   - Supports sorting by:
     - `price` (ascending or descending).
   - Always sorted by `startingDate` in ascending order after applying filters.

---

## Models

### **Users**
- `ID`
- `Email`
- `Password`
- `Roles` (Many-to-Many relationship)

### **Roles**
- `ID`
- `Name`

### **Travels**
- `ID`
- `isPublic` (boolean)
- `Slug`
- `Name`
- `Description`
- `Number of Days`
- `Number of Nights` (virtual, computed as `numberOfDays - 1`)

### **Tours**
- `ID`
- `travel_id` (Many-to-One relationship with `Travels`)
- `Name`
- `Starting Date`
- `Ending Date`
- `Price` (integer, stored as cents)
- `Notes`

---

## Additional Notes
1. Use Laravel's native authentication.
2. **UUIDs** as primary keys are highly appreciated but not required.
3. Store tour prices as integers multiplied by 100 (e.g., €999 becomes `99900`).  
   When returning to frontends, format as `price / 100`.
4. Admin users must also have the editor role.
5. Creation endpoints must only create **one resource per request** (no bulk creation).
6. Usage of tools like `php-cs-fixer` and `larastan` is a plus.
7. Writing documentation is a **big plus**.
8. Writing feature tests is a **big, big plus**.
