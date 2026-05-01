##### Child Prompt: Implementing a Product Search and Filtering API Endpoint



###### 1\. Context

Based on the Parent Prompt guidelines, you are tasked with implementing a search and filtering API endpoint for the Catalog Module of the monolithic ASP.NET Core application. This endpoint should allow clients to retrieve products based on various criteria such as name, category, price range, and availability, with support for pagination and sorting.



###### 2\. Task Requirements

2.1. Endpoint

HTTP Method: GET



Route: /api/v1/products/search



Authorization: Allow anonymous access (unless business rules require otherwise).



2.2. Query Parameters

searchTerm (optional): Filter by product name or description.



categoryId (optional): Filter by category.



minPrice and maxPrice (optional): Filter by price range.



isActive (optional): Filter by active status.



pageNumber (default: 1): Pagination support.



pageSize (default: 10): Pagination support.



sortBy (optional): Field to sort by (e.g., name, price, created).



sortDescending (optional): Sort direction (default: false).



2.3. Implementation Details

Use CQRS with MediatR to encapsulate the logic in a query and handler.



Use FluentValidation to validate query parameters (e.g., ensure minPrice ≤ maxPrice).



Use EF Core for data access with optimized queries (e.g., AsNoTracking(), projection).



Implement caching (e.g., IMemoryCache) for frequently accessed search results.



Ensure pagination using the PaginatedList<T> pattern (as shown in the Parent Prompt).



Use API versioning (v1) and document the endpoint with Swagger/OpenAPI.



2.4. Code Structure

Create a query class GetProductsSearchQuery in Application/Products/Queries.



Create a handler GetProductsSearchQueryHandler in the same location.



Add validation rules in GetProductsSearchQueryValidator.



Add the endpoint to the ProductsController in Web/Controllers/Api/V1.



2.5. Testing

Write unit tests for the query handler and validation logic.



Write integration tests to verify the endpoint behavior.



2.6. Performance \& Security

Ensure database queries are optimized (indexes, minimal data retrieval).



Sanitize input to prevent SQL injection or other attacks (EF Core parameterization is sufficient).



###### 3\. Expected Output

3.1. Code Files

GetProductsSearchQuery and GetProductsSearchQueryHandler.



GetProductsSearchQueryValidator.



The corresponding endpoint in ProductsController.



3.2. Tests

Unit tests for the handler and validator.



Updates to the ProductsController to include the new endpoint.

