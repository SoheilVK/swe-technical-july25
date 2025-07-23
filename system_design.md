# System Design Challenge: External API Integration

## Problem Statement
Design a system to efficiently fetch and update event ticket data from a third-party supplier's API while respecting strict rate limits and handling large data volumes.

We need to regularly synchronize ticket listings from a third-party tickets provider's API with our internal system. The challenge is to maximize update throughput while staying within the API's constraints and ensuring data freshness across thousands of events.

## Technical Constraints

### API Limitations
- **Rate Limit**: 500 requests per minute (global limit across all operations)
- **Pagination**: Each API request returns one page of results
- **Page Size**: Maximum 200 tickets per page
- **No Parallel Processing**: The rate limit is global, meaning all requests count toward the same pool

### Data Volume Characteristics
- **Event Scale**: Thousands of events in our system require regular updates
- **Ticket Volume**: Popular events can have 4,000+ tickets (requiring 20+ API requests per event)
- **Update Frequency**: Need to keep ticket data reasonably fresh across all events