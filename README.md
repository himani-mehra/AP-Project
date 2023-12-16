# Vue.js Acharya Prashant Web Page Replica

## Project Overview

This Vue.js project aims to replicate the Acharya Prashant web page [here](https://acharyaprashant.org/en/courses/series/course-series-eeb9d3). The project fetches data from three API endpoints to populate the content.

### What the Project Does

- Recreates the layout and design of the Acharya Prashant web page.
- Utilizes three API endpoints to fetch data:
  - [Course Series Data](https://api.acharyaprashant.org/v2/legacy/courses/series/optuser/course-series-eeb9d3)
  - [Course Tags](https://api.acharyaprashant.org/v2/legacy/courses/tags)
  - [FAQs](https://api.acharyaprashant.org/v2/legacy/courses/faqs?language=english)

## How to Use

1. Clone the repository:
    bash
  git clone https://github.com/himani-mehra/acharya.git
   
2. Navigate to the project directory:
       cd Vue_project

3. Install dependencies:
   npm install
   
5. Run the development server:
     npm run dev

6. Open your browser and visit http://localhost:8080 to view the replica.


## Project Details
  The project was created to replicate the Acharya Prashant web page using Vue.js , as a given assignment to me . I was provided with a reference webpage , to assess my frontend skills of html, css, JS framework. 
  ### Features: Responsive design
  Data fetched from API endpoints
  ![image](https://github.com/himani-mehra/acharya/assets/73715725/18fecfb8-c891-4762-9f50-179c331f2cd2)
![image](https://github.com/himani-mehra/acharya/assets/73715725/accc8821-d0dc-45a2-b1fe-8b91827f8dd3)
![image](https://github.com/himani-mehra/acharya/assets/73715725/0be3bc71-3030-4168-a32c-c9c07a062022)



  ### Challenges Faced:
I picked up bottom up approach and hence started with the integration of FAQ section API. but as I reached to top and began integrating the search bar           API , I faced issues in displaying in the similar  manner as specified in the refernce page , however , data is picked up perfectly from the             API and the mapping is also working fine (Parent to child mapping).
 
  ### Proud Achievements: 
  I gained confidence as I completed the page within 1.5 days of assignment day , maining attention to details (as you can observe the minute details in arrow icons , naming conventions, code formatting , code cleaning , or social media icons changing on mouse hover , transion timing , providing href for all buttons) however , I was stuck the the UX for search popup modal issue.

  ### Technologies Used:
  HTML , CSS , Vue.js

  ### Future Plans :
  Will fix the  UX for search modal popup

  ## Contact : Himani Mehra
   GitHub Profile: https://github.com/himani-mehra 
   Linkedin Profile: https://www.linkedin.com/in/himani-mehra/
  
  


    



