#Todo App Lab
---

We're going to take a basic Rails app and add models specs, a controller and controller specs to it. 

Below are the steps (with details) of what has been _already_ done in this app.

Copy `todo` into your source code folder. Then, take a moment with your partner and get familiar with what has already been setup.

Once you're familiar, run through the step by step lab below. The steps are the order a normal developer would take to setup a basic app.

##Steps Already Completed.
---

Make sure you understand what the codebase looks like right now. Go through these steps so you know what is going on.

1. Setup Rspec

    Add required Gems to our Gemfile.

    ```
    # Gems above removed for brevity.

    gem 'rspec-rails', '~> 3.1.0'
    ```

    Then

    ```
    $ bundle install
    ```

    Once everything is bundled, use rails generator to install Rspec 

    ```
    $ rails generate rspec:install
    ```

2. Init git!

    ```
    $ git init
    $ git add .
    $ git commit -m 'Initial commit woooo'
    ```

    Then go to Github and create a new repo under your account (the `+` at the top-right). Since git is already initialized you can copy and paste the part that says "Setup an existing repo". 

    After your remote is setup:

    ```
    $ git push -u origin master
    ```

    Now, commit and push whenever you have made progress for the rest of this project.

3. Generate our Task model. We probably want to have a name and complete.

    ```
    $ rails g model Task name complete:boolean
    ```

4. Let's also add Bourbon now.

    Add the gem:

    ```
    # Gems above removed for brevity.

    gem 'bourbon'
    ```

    Then follow the Bourbon instruction to install it:

    ```
    $ bundle install
    ```

    Then we want to rename our application.css to be a Sass (`.scss`) file:

    ```
    mv app/assets/stylesheets/application.css app/assets/stylesheets/application.scss
    ```

    And finally remove all the Sprocket directives and use Sass's import syntax to import Bourbon in the `application.scss` file:

    ```
    /*
     * This is a manifest file that'll be compiled into application.css, which will include all the files
     * listed below.
     *
     * Any CSS and SCSS file within this directory, lib/assets/stylesheets, vendor/assets/stylesheets,
     * or vendor/assets/stylesheets of plugins, if any, can be referenced here using a relative path.
     *
     * You're free to add application-wide styles to this file and they'll appear at the bottom of the
     * compiled file so the styles you add here take precedence over styles defined in any styles
     * defined in the other CSS/SCSS files in this directory. It is generally better to create a new
     * file per style scope.
     *
     *= require_tree . # REMOVE THIS
     *= require_self   # REMOVE THIS
     */

     @import "bourbon"; # ADD THIS
     # ADD ANY OTHER STYLESHEETS YOU CREATE IN THE FUTURE BELOW @import 'bourbon'.
    ```

5. Lets install Bitters too!

    Add the Gem.
    
    ```
    gem 'bitters'
    ```

    Then cd into the stylesheets directory and install Bitters there.

    ```
    $ cd app/assets/stylesheets
    $ bitters install
    ```

    Finally add Bitters below Bourbon in our `application.scss`:

    ```
    # The rest of the file ommitted for brevirt

    @import 'bourbon';
    @import 'base/base'; # ADD THIS
    ```

6. Lets setup our database quick.

    ```
    $ rake db:create
    $ rake db:migrate
    ```

    Remember, we already made a model so we need to migrate the DB.

7. A homepage would be nice. We can make a `Home Controller` with an `index` action for the homepage of our app.

    ```
    $ touch app/controllers/home_controller.rb
    ```

    Fill out that file with a basic home controller.

    ```
    class HomeController < ApplicationController

    end
    ```

    We don't need the action to be defined, which is cool. Essentially, if you don't need to write any action logic, Rails doesn't mind :) Just write the route to the controller and give the view file the correct name.

    Route first!

    ```
    Rails.application.routes.draw do

      root to: 'home#index'

    end
    ```

    Now the view!

    ```
    $ mkdir app/views/home
    $ touch app/views/home/index.html.erb
    ```

    Add some text to the view:

    ```
    <h1>Welcome to Todo</h1>
    Yay! This is marketing copy!
    ```

8. Start up the server and just make sure we're all good.

    ```
    $ rails server
    ```

    Go to your browser. You can also do a shortcut using Unix. In a new tab in Terminal:

    ```
    $ open http://localhost:3000/
    ```

##Start Here - Do These
---

Cool! That is all the prep work in the project. Now work on the tasks below. Go through this lab and complete these tasks in order.

###A little pre-work: make sure your Gems are bundles and your DB is created and migrated.

1. Create an empty **Model Spec** for Task (hint: there is a generator for this.)

2. Write a spec that asserts a Task should be valid with all the required fields.

3. Write a spec that asserts a Task isn't valid without a name

4. Add validations for your Task model only to make the name test pass

5. Write a spec that asserts a Task isn't valid without a complete

6. Write a validation for your Task mode to make the complete test pass

7. Write a spec that asserts a new Task has a default value of `false` for complete

8. Write a model callback for your Task to make the default value for complete pass

###Now, we switch to the Task Controller Spec.

9. Create an empty **Controller Spec** for the Tasks Controler.

10. Write a spec for `GET index` that asserts the response is successful

11. Create the routes for the Task Controller we haven't made yet

12. Create the Task Controller and index action

13. Create the index view for the index action.

14. Make sure our only controller spec passes.

15. Write a spec that asserts `GET index` renders the index file

16. Create two tasks in your spec using `let!`. Make sure your spec still runs afterward.

17. Write a spec that asserts `GET index` creates a variable named `tasks` and that variable includes the two tasks you created.

18. Don't go on until your spec passes and you feel confident the TasksController `GET index` action is working.

19. Write a spec for `GET new` that asserts the response is successful.

20. Write an action and view for the test to pass.

21. Write a spec that asserts `GET new` renders the new file.

22. Make sure the test passes.

23. Write a spec that asserts `GET new` creates a variable named `task` and that the variable's class is a `Task` (and, implicitly, not a different model).

24. Adjust your new action to get those specs to pass.

25. Write a spec that asserts `GET new` does not create a new Task in the database.

26. Make sure that test passes.

27. Write a describe block for `POST create`.

28. Write a context for `when form is valid`.

29. Write a context for `when form is invalid`.

30. Use `let!` to create a hash of valid attributes inside the valid attributes context.

31. Write a spec that asserts `POST create` (when attributes are valid) creates 1 new Task in the database.

32. Write a spec that asserts `POST create` (when attributes are valid) redirects to the index page.

33. Adjust your create action to make those two _valid_ tests pass.

34. Write a spec that asserts `POST create` (when attributes are not valid) does not create any new Tasks in the database.

35. Write a spec that asserts `POST create` (when attributes are not valid) renders the new file.

36. Adjust your create action to make those two _invalid_ tests pass.

37. Write a spec that asserts `DELETE destroy` redirects to the index action.

38. Use `let!` to create a yogurt so we can destroy it.

39. Create the destroy action and add logic to make that test pass.

40. Write a spec that asserts `DELETE destroy` changes the number of Tasks in the database by 1.

41. Add logic to make that test pass.

42. Write a spec to assert `DELETE destroy` assigns the yogurt you creates to a variable yogurt.

###Once all your tests pass, you know the logic of your app works. Now you can spend time stylging your app!

43. Add links to your views so users can easily navigate around your site.

44. Add a link to each task on the index page for marking the task as done.

45. Add a link to each task on the index page to delete the task.

46. Add a count of all the tasks a user has finished.