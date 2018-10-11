<template>
  <q-page class="flex">
    <q-card class="fit text-center" flat style="border-top: 4px #4CA751 solid;">
      <q-card-title>
        <h5 style="color: #4CA751;">
          Systems Application Programmer
        </h5>
        <div style="line-height: 18px; font-size: 12px;">
          <div>3444 N 2650 E Layton, UT 84040</div>
          <div>Telephone: (801) 243-9739</div>
          <div>E-mail: trevororgill80@gmail.com</div>
        </div>
      </q-card-title>
      <q-card-main>
        <q-list no-border>
          <q-item>
            <q-item-side style="font-weight: bolder; font-size: 1.5em;">Summary</q-item-side>
          </q-item>
          <q-item>
            <q-item-main>Dynamic and motivated professional generating and building relationships, managing projects from
              concept to completion, and designing educational strategies. Skilled in building cross-functional teams,
              demonstrating exceptional communication skills, and making critical decisions during challenges.
              Adaptable and transformational leader with an ability to work independently, creating effective
              presentations, and developing opportunities that further establish organizational goals.</q-item-main>
          </q-item>
          <q-item-separator/>
          <q-item>
            <q-item-side style="font-weight: bolder; font-size: 1.5em;">Experience</q-item-side>
          </q-item>
          <q-item v-for="(experience, index) in experience" :key="'r' + index">
            <q-item-main>
              <span style="color: #4CA751;">{{ experience.title }}</span>
              <q-item-tile style="color: #B7B7B7;">{{ experience.location }}</q-item-tile>
              <q-item-tile>{{ experience.description }}</q-item-tile><br/>
              <q-item-tile style="color: #B7B7B7;">Responsibilities</q-item-tile>
              <q-item-tile>
                <q-list no-border dense>
                  <q-item v-for="(responsibility, index2) in experience.responsibilities" :key="'rs' + index2">
                    {{responsibility}}
                  </q-item>
                </q-list>
              </q-item-tile>
            </q-item-main>
          </q-item>
          <q-item>
            <q-item-side style="font-weight: bolder; font-size: 1.5em;">Education</q-item-side>
          </q-item>
          <q-item v-for="(education, index) in education" :key="index">
            <q-item-main>
              <span style="color: #4CA751;">{{ education.school }}</span>
              <q-item-tile style="color: #B7B7B7;">
                {{ education.degree }}
              </q-item-tile>
              <q-item-tile style="color: #B7B7B7;">
                GPA: {{ education.gpa }}
              </q-item-tile>
            </q-item-main>
          </q-item>
          <q-item-separator/>
          <q-item>
            <q-item-side style="font-weight: bolder; font-size: 1.5em;">Skills</q-item-side>
          </q-item>
          <q-item v-for="(skill, index) in skills" :key="'sa' + index">
            <q-item-main>
              <span style="color: #4CA751;">{{ skill.type }}</span>
              <q-item-tile>
                <span v-for="(s, index2) in skill.skills" :key="'s' + index2">
                  {{ s }}<span v-if="index2 !== skill.skills.length - 1">,</span>
                </span>
              </q-item-tile>
            </q-item-main>
          </q-item>
          <q-item-separator/>
        </q-list>
      </q-card-main>
    </q-card>
  </q-page>
</template>

<style>
</style>

<script>
export default {
  name: 'PageIndex',
  data () {
    return {
      experience: [{
        title: 'Systems Application Programmer - Weber State University',
        location: 'Ogden, Utah - August 2017 - Present',
        description: 'Full stack developing from the database, backend, frontend. Providing work for interns, so that as a team we can keep productive and effective work. Took part in the planning and implementation of a secure testing software product.',
        responsibilities: [
          'Take in feedback to better shape our product.',
          'Work as a team to create a plan for our product.',
          'Give interns directions and help.',
          'Supporting already active products.'
        ]
      },
      {
        title: 'Freelance Work',
        location: 'Utah - June 2016 - Present',
        description: 'Work with the customer, to create/manage and deliver a product. This gives valuable experience that cannot be taught, but only learned.',
        responsibilities: [
          'Work directly with clients.',
          'Manage and create a plan for a product to be created.',
          'Implement the product teh client wants.',
          'Present and support the created application.'
        ]
      },
      {
        title: 'Programming Intern - Weber State University',
        location: 'Ogden, Utah - May 2016 - August 2017',
        description: 'Worked with a team in a real world environment, as well as having direct contact with customers and working with them to fix/create features that they wanted.',
        responsibilities: [
          'Provide technical support to customers using our software.',
          'Implement bug fixes to our current system.',
          'Work on browser related applications.',
          'Code for the creation of a new testing application.'
        ]
      },
      {
        title: 'Graphics Designer - Interstate Image',
        location: 'Salt Lake City, Utah - June 2015 - August 2015',
        description: 'Part of the shop crew, in charge of preparing graphics and installing graphics for vehicles, and walls. This environment allowed me to build great team building skills. As well as the opportunity to work with customers to insure they get exactly what they wanted.',
        responsibilities: [
          'Prepared and installed vinyl graphics for installation on vehicles and walls.',
          'Working independently to production and mailing of graphics produced.',
          'Worked independently to produce and ship out graphics.'
        ]
      },
      {
        title: 'Lifeguard/Water Safety Instructor - Clearfield Aquatic Center',
        location: 'Clearfield, Utah - May 2012 - May 2014',
        description: 'Being a lifeguard teaches you how to be a leader, and how to maintain composure under pressure.',
        responsibilities: [
          'Manage schedules, and position charts for other lifeguards on duty.',
          'Customer service representative for the recreational center.',
          'Work as a team to help kids and other WSI instructors to meet their goals.'
        ]
      }],
      education: [{
        school: 'Weber State University',
        degree: 'Bachelor\'s Degree, Computer Science',
        gpa: '3.6'
      },
      {
        school: 'Weber State University',
        degree: 'Associate of Applied Science, Computer Science',
        gpa: '3.59'
      }],
      skills: [{
        type: 'Programming Languages',
        skills: ['SQL', 'NoSQL', 'Java', 'Javascript', 'HTML5', 'CSS', 'C', 'C#', 'JQuery', 'Git', 'Angular', 'React', 'Vue', 'Coldfusion', 'Swift', 'Python', 'Bash', 'Ruby']
      },
      {
        type: 'General Knowledge',
        skills: ['Teamwork', 'Management', 'Leadership', 'Technical Support', 'Customer Service']
      }]
    }
  }
}
</script>
