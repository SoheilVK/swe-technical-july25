# Coding Challenge: Rate-Limited API Client

## Scenario
We often integrate with external APIs that have strict rate limits and occasional failures. Your task is to implement a Python solution that calls an API while respecting these constraints.

## Requirements

1. **Rate limiting**: Ensure no more than 5 requests per minute
2. **Retry logic**: Implement retry behavior for failed requests (you decide the strategy)
3. **Statistics tracking**: Monitor and report:
   - Total requests attempted  
   - Successful requests
   - Failed requests (after retries are exhausted)
4. **Error handling**: Handle failures gracefully without crashing
5. **Demonstration**: Show your solution working with 10 API calls

## API Simulation

Use this function to simulate the external API:

```python
import random
import time

def mock_api_call():
    time.sleep(0.1)  # Simulate network delay
    if random.random() < 0.8:  # 80% success rate
        return {"status": "success", "data": "some_data"}
    else:
        raise Exception("API call failed")
```

## Discussion Points
Be prepared to discuss:
- Your design choices and trade-offs
- How you would modify this for production use
- Edge cases you considered
- How you would test your implementation