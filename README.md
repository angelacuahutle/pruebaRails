# README

This README would normally document whatever steps are necessary to get the
application up and running.

Things you may want to cover:

* Ruby version

* System dependencies

* Configuration

* Database creation

* Database initialization

* How to run the test suite

* Services (job queues, cache servers, search engines, etc.)

* Deployment instructions

* ...

**Road map**

- git flow
  - development < feature
- rails new
  - postgres
  - rspec  
- Add test to it
  - Unit tests
    - Validations
    - Associations (if required)
  - Controller test 
    - index
- Add devise
  - Devise generic tests
- Add necesary gems 
- Generate models
- Run migrations 


## Pruebas

  unit
    associations
      user has many courses, can only enroll once
      courses belongs to admin, class User
    students << devise
      validates presence, uniqueness
        full_name
        email format
        password
      devise tests
        login
    courses
      validates presence
        name
        teacher
        started_at
  requests
    admin#index
      @students = Student.all
      @courses = Course.all
      forms
        create user
        create course
        delete existing elements  
    user#login
    user#index
      @enrolled_courses = current_user.courses.sort_by(:started_at)
      @other_courses = Course.all.sort_by(:name)
    course#enrollment
      current_user.build(@course).save!
    courses#index
      courses#show
  system
    enrollment
      visit course#show page
      it shows name
      it shows teacher's name
      it shows started_at
      it shows enrolled students sort_by(:name)
      when not enrolled
        within 'other courses' do
          click_button 'Enroll'
          expect current_user.courses to include course
        end
      when enrolled
        within 'enrolled_courses' do
          expect(find(#enroll)).to be disabled
        end
    admin # Add instruction to create admin user to README.md
      permissions
        can manage students
          create, delete, edit*
        can manage courses
          create, delete, edit*
