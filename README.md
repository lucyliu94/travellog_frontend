# Capstone (Front-end)
## by Lucy Liu

## Explanation of App
Finally a centralized location for you to house all your travel activities. You can filter through and see some of your favourite destinations and relive your memories! 


## Technologies Used
- Svelte
- Express
- Bootstrap
- CSS
- HTML

## Libraries/Techniques
- Front-end CRUD functionality, REST API
- Backend API Deployment with Heroku
- Frontend React Deployment with Vercel
- Font-Awesome Icons


## Routing Table 

#### Main
| Action         | Path                        | Request   | Purpose                                                                        |
|:--------------:|:---------------------------:|:---------:|:------------------------------------------------------------------------------:|
| Index          | /travellogs                   | GET       | List all entries                                                   |
| Edit           | /editTravellogs/:id              | PUT       | Edit the entry's detail in the form                                                |
| Delete         | /travellogs                   | DELETE    | Delete the entry                                                        |
| Create         | /travellogs                | POST      | Create a new entry                                                     |




## User Stories

- Users will be able to view a full list of all their travel logs once they visit the site
- Users will be able to create, read, update, or delete their logs
- Users can create a new log by clicking on new log to make new entries
- Users can click on each individual entry to edit each travel log by submitting through the form
- Users can delete by clicking on the icon to remove entry

## Challenges
- I originally wanted to add authentication but figuring out the icon library importation and getting used to the overall Svelte language took a bit longer than I imagined so to meet MVP I decided to leave out authentication for now.
- I had some issues implementing a modal for the form. I opted to leave it as a form but would want it have a more 3D look going forward by implementing it as a modal
- I thought I could link a CSS file to have one centralized place for styling but I ended up having some issues with deployment so I just used the style tags and placed my css styling there for each page. 
- Styling issues with the form as the checkbox wouldn't align left - so I texted to align all the input and text center to make it look less odd on the screen
