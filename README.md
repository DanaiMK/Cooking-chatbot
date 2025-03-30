# Cooking-chatbot
A task-oriented dialog system built in the cooking domain using Rasa. It assists users in searching for recipes based on dietary restrictions or available ingredients and even provides a detailed Moussaka recipe 


## Presentation

You can view the project presentation here: https://docs.google.com/presentation/d/1wOrdDCH02A6KbBpI0vS-Sn9hL1njzzJhjSnrtXnstFM/edit?usp=sharing



# Motivation
The cooking domain was chosen because many people need quick and easy access to recipes and cooking ideas. Users often have specific dietary requirements (e.g., vegan, vegetarian) and available ingredients at home. This chatbot aims to assist users by providing tailored recipe suggestions and detailed instructions, thereby enhancing their cooking experience.

# Integrated Data Sources Details

**Spoonacular API:**  
The chatbot integrates with the Spoonacular API to fetch real-time recipe data based on dietary restrictions and ingredients. 


# Dialog Policy Experimentation

During the development of Pepito, we conducted several experiments to improve the dialogue policy. Below are the details of the changes we made, the rationale behind these modifications, and the observed results and insights:


# The Changes Made


- **Data Validation:**  

We implemented checks to ensure that the data returned by the API contains the expected fields before processing it.

For example, before processing the API response, we verify that the JSON object contains the key `"results"` and that it is non-empty:

This prevents the bot from trying to process incomplete or unexpected data.


- **Enhanced Fallback Messages:**  

We improved the fallback messages to be more specific, providing clear feedback based on the type of error encountered. 

For instance, if an API call fails due to a network issue, instead of a generic error message, the bot now displays:

"It seems there's a network issue. Please try again in a few moments."

This ensures that the user understands the nature of the problem and can act accordingly.


- **Rules Enhancement**

To improve the overall conversation flow and ensure consistent responses, we introduced a comprehensive set of explicit rules in our dialog policy configuration. Instead of relying solely on the stories to manage the dialog flow, these rules directly map key user intents to their corresponding actions. This enhancement covers scenarios such as:

- Ending the conversation when the user wishes to stop the recipe search.
- Providing additional recipe options when requested.
- Handling queries related to dietary restrictions and ingredient-based searches.
- Delivering detailed recipe information on demand.

After implementing these rules, the chatbot consistently follows the intended flow without getting confused by overlapping scenarios.


- **NLU Enhancements**

To improve the performance of the NLU model, we significantly increased the number and diversity of training examples for each intent in our dataset.

We augmented our NLU training data by adding numerous examples for each intent such as `choose_search_type_dietary`, `provide_dietary_restriction`, `choose_search_type_ingredient`, `provide_main_ingredient`, etc.



### Demonstrations of the chatbot’s capabilities

Below there is an implementation of the chatbot capabilities.

Your input -> hi
Hi! I'm Pepito, your personal cooking assistant! You can ask me for recipes based on your available ingredients, dietary preferences or calories limit. How would you like to proceed?
Your input -> I need vegan recipes
Got it! You're looking for vegan recipes.
I found a vegan recipe: Asparagus and Pea Soup: Real Convenience Food.
Would you like more info about preparation and cooking time?
Your input -> That's enough
Got it! Let me know if you need anything else. Happy cooking!


## Limitations and Future Improvements


- **Free API Constraints:**  
  The current implementation uses a free version of the Spoonacular API. While this allowed us to integrate dynamic recipe data, the free tier imposed limitations on the number and variety of recipe options available. Consequently, some features and detailed information (such as a broader range of recipes or more specific filtering options) could not be fully implemented.

**Future Improvements:**
- **Enhanced Data Sources:**  
  To overcome the limitations of the free API, a future improvement would be to integrate with a more comprehensive or paid API service. This would provide access to a larger dataset and more detailed recipe information.
  
- **Additional Scenarios:**  
  One specific area for future enhancement is the implementation of additional scenarios, such as:
  - **Calorie-based Recipe Suggestions:**  
    Developing a feature that displays recipes based on calorie content. Currently, due to the limitations of the free data available, this functionality could not be implemented. With access to more detailed nutritional data, the bot could offer personalized meal suggestions based on caloric needs.
  
- **Improved Personalization:**  
  Further improvements could include more advanced filtering options (e.g., dietary restrictions combined with calorie counts, ingredient availability, or cuisine types) to provide more tailored recipe recommendations.

- **Enhanced Error Handling and Caching:**  
  Additional mechanisms such as advanced caching strategies or a more sophisticated error handling system (e.g., using a circuit breaker pattern) could further enhance the reliability and responsiveness of the chatbot.

By addressing these limitations and implementing the suggested improvements, future iterations of the chatbot will be able to provide a richer and more personalized user experience.


## Setup of API Keys and Environment Variables

This project requires API keys to access external data sources (the Spoonacular API).

1. **Obtain an API Key:**
   - Visit [Spoonacular API](https://spoonacular.com/food-api) and sign up for a free account.
   - Obtain your API key from your account dashboard.

2. **Create a `.env` File:**
   - In the root directory of the project, create a file named `.env`.
   - Add the following lines to the file, replacing the placeholder with your actual API key:
     ```env
     API_KEY=your_recipe_api_key
    
     ```
3. **Ensure the `.env` File is Not Tracked:**
   - Make sure that the `.env` file is added to your `.gitignore` file so that your keys are not exposed in the repository.

4. **Usage:**
   - The application will automatically load these environment variables when it starts, allowing the custom actions to use them for API calls.



