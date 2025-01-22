Driveway

1. Developed the main customer facing E-commerce shop page (implemented with React Typescript in Next.js framework).

How did we use React

- The framework the whole app revolved around, prioritzing reusability of components in the userface that had to repeat frequently

How did we use Typescript:

- Was helpful for tracking all the different forms of expected inputs and outputs of data and used to document what each domaine and component was expected to handle in terms of state and user interactions.

How did we use Next.js

- implemented within the final year of the mass layoff, we switched our domains of the site to utilizing layouts for better load time. I had switched to helping the checkout flow at this time so it was especially helpful for managing the order of forms and monitoring where they were in the process

2. Worked on Search Results Page, Vehicle details page and Vehicle Gallery pages

3. Fulfilled features: Purchase Pending / In Transit, shop New Cars, Approval Likelihood, Vehicle Gallery, and so much more.

- Purchase Pending/In transit = Here I added a property to be expected back from the API (collaborated with backend to confirm variable name and shape of data) to graphql and added a component that would lable which vehicles were in transit to dealerships or recently in the process of being purchased by other users. Then I added the functionality within the components that present the car data (search results page and details page) to conditionally render depending on the presence of that data and limit the functionality of the user flow for the vehicles that would be potentially unavailable (purchase pending)
- New Cars was its own version of the shop search results page that required its own sets of filters and slightly different variants of vehicle cards. We had to ensure we had broken up vehicle cards into components that could be used by all variants while not overcomplicating the code, and same with the filter UI. We also had to persist filters that were set between the two versions: used or new cars. Filters that were especially different: Mileage, year range,

4. Increased Search pages lighthouse scores by 40% with integration of Zustand state management.

- implementing the statemanagement for filters on the search results page reduced a lot of memory we were taking up for default values in our filters. If the user hadn't made a change to a filter we were no longer setting a value on their page arival, and the components knew what to show without explicitely having the default state being set. The query's were also streamlined for default values. There were specific filters that would have side effects to toggling other filters (green cars), and the logic for this was also streamlined with the power of zustand state management with their reactive functions. Before this we were just using react context and useState's to set the filters and their values. in a giant container component for all the filters. When we had to implement new car, the complexitiy here was about to intensify, leading to us looking for a solution like zustand and ended up severly cleaning up and organizing our filter and component logic

5. Raised shop domains test coverage from 12% to 75% with jest tests within 2 quarters.

- This was done mainly by organizational virtue and adding a requirement in the story lifecycle process for our agile work environment to require new components and modified components have full test coverage for their functionality covered by the story (and prior ones). After the initially workload of creating mock contexts and hooks in jest, adding tests became a lot faster and we were soon back up to speed and more confident that we weren't regressing previous functionality as we were completing new stories.4

6. Leadership: Led the retrospectives of all the teams I was involved in to prioritize progressive team development and health.

- I enjoyed hosting retrospectives because I really enjoyed ensuring everyone got a chance to voice their perspective of what was working and not working well in relation to the previous sprint, as well as giving kudos to team members for their contributions. It seemed to create great team comradery, start good conversations about how to best handle processes and learn from things that didnt turn out great, and keep everyone pointed to a common north star. Hosting the space for everyone to be heard felt very rewarding and it made me feel fulfilled to see us all working well in our direction together every sprint.

7. Operated in 2 week sprints, coordinating with designers, product managers and QA engineers in refinement meetings to
   clarify ACs of user stories for accuracy of product fulfillment.

- We had a number of ceremonies throughout the sprint: every morning we had standup to vocalize what everyone was working on and ensure no one was stuck (or if so, get them unstuck after the meeting), at the beginning of every sprint we added storys that had been assessed and pointed to "the board", a few days after we had story planning sessions where we would ask any questions as engineers about stories that may be vague in some aspect to assure it had as much specification and clarity as needed to be executed in the code, we would have tech debt meetings to do a similar process but with code efficiency purpose rather than project manaegemnt purpose, and assign them out to engineers, and then we would have retrospectives at the end of every sprint.
