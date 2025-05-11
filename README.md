# whois-lookup
whois-lookup
This WHOIS lookup tool includes:

Input Validation:

Regex validation for domain names
Error messaging for invalid inputs
Enter key support for quick searches
Search Functionality:

Loading state with spinner
Mock API response simulation
Recent search history stored in localStorage
Results Display:

Clean, organized presentation of WHOIS data
Responsive grid layout for key information
Formatted dates for better readability
Status and nameserver lists
User Experience:

Recent search suggestions
Clear error states
Helpful informational text
The component is fully responsive and uses Tailwind CSS for styling. The mock data provides a realistic example of what a WHOIS API might return, including registrar information, dates, status codes, and nameservers.

In a production environment, you would replace the mock API call with an actual WHOIS API endpoint. The component is structured to make this easy - just replace the setTimeout with your API fetch logic

Key Changes for Real API Integration:
API Configuration:

Added constants for API key and endpoint
Using WHOISXMLAPI's free tier service
API Fetch Function:

Created fetchWhoisData function that makes real API calls
Handles both successful responses and errors
Processes the JSON response
Data Extraction Helpers:

Added helper functions (getRegistrar, getNameServers, getStatus) to handle varying response structures
Different WHOIS APIs may structure their responses differently
Error Handling:

Better error handling for API failures
Displays API error messages to users when available
API Limitations Notice:

Added disclaimer about free tier limitations
Important Notes:
API Key:

You'll need to sign up at whoisxmlapi.com to get a free API key
Replace your_free_api_key_from_whoisxmlapi with your actual key
In production, use environment variables to store the API key
Rate Limiting:

The free tier has limits (1000 requests/month)
Consider implementing client-side rate limiting
Response Structure:

The code handles the WHOISXMLAPI response structure
If you use a different provider, you'll need to adjust the data extraction
Privacy Considerations:

Be transparent about data usage
Consider adding a privacy policy if collecting user data
This implementation now provides real WHOIS data instead of mock data, giving users accurate domain registration information.

Key Fixes for 401 Error:
Proper API Key Setup:

Get a valid API key from whoisxmlapi.com
For development, you can use their test key: at_test123 (but will only return mock data)
For production, sign up for a free account (1000 requests/month)
Environment Variables (Recommended):

# .env.local
NEXT_PUBLIC_WHOIS_API_KEY=your_actual_key_here
Enhanced Error Handling:

Specific messages for 401 (invalid key) and 429 (rate limit) errors
Better response status checking
Proper API Request Format:

Using URLSearchParams for correct parameter encoding
Added Accept header for JSON responses
Common Solutions for 401 Errors:
Invalid/Expired API Key:

Verify your key at whoisxmlapi.com account dashboard
Regenerate if necessary
Incorrect Parameter Name:

WHOISXMLAPI expects apiKey (case-sensitive)
Some services use key or token
Missing Parameters:

Ensure all required params are included:
{
  apiKey: 'your_key',
  domainName: 'example.com',
  outputFormat: 'JSON'
}
IP Restrictions:

Check if your API key has IP restrictions
Some services require whitelisting your server IP
Testing Your API Key:
You can verify your key works by making a direct request:

curl "https://www.whoisxmlapi.com/whoisserver/WhoisService?apiKey=YOUR_KEY&domainName=google.com&outputFormat=JSON"
Remember to never expose your API key in client-side code in production. For a production app, you should:

Create a backend proxy endpoint
Store the API key server-side
Have your frontend call your own endpoint
Would you like me to show you the backend proxy implementation as well? This would be the most secure approach for a production application.
