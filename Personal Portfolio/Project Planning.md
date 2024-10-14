**Requirements**
- I can login and signup
- I can add my projects
- I can add my Personal Info
- I can add my experience
- I can add my achievement
- I can add my resume
- I can add my Skills
- I can view my profile with complete details
- I can share my public profile link


**DB Design**
- Person
	- personId (long, primary key)
	- userName(varchar)  %%public view%%
	- name (varchar)
	- email (varchar) %%validate%%
	- mobile Number (number,Optional)
	- imageUrl(varchar)
	- resumeUrl(varchar,optional)
- Projects %%this is mapped many to one with person%%
	- projectId (long, primary key)
	- personId (long, foreign key)
	- projectName(varchar)
	- projectDesc(varchar)
	- projectImageUrl(varchar)
	- repoUrl(varchar)
	- startDate(varchar)
	- endDate(varchar)
	- skillUsed(varchar) %%separated by '|' ex => "java|python|mysql"%%
- Experiences %%this is also many to one with person%%
	- experienceId(long,primary key)
	- personId(long,foreign key)
	- employerName(varchar)
	- location(varchar)
	- startDate(varchar)
	- endDate(varchar,optional)
	- skillUsed%%separated by '|' ex => "java|python|mysql"%%
	- currentlyWorking(tinyInt)%%0 or 1%%
- Skills %%this is universal and any personal can use same skill %%
	- skillId (long, primary key)
	- skillName(varchar,unique)
	- skillLogoUrl(varchar)
- Achievement %%each is mapped with person many to one %%
	- achievementId(long,primary Key)
	- name
	- provider
	- certificateUrl
	- achievedDate

**Functional Requirements**
- I can signup/login to website
- I can create my profile
- I can add my experience/achievements/skills/projects/resume etc
- I can update my details

**API required**
- /api/v1/person/signup
- /api/v1/person/login
- /api/v1/person/forgot_password
- /api/v1/person/{username}/experience
- /api/v1/person/{username}/project
- /api/v1/person/{username}/achievement
- /api/v1/skill

**API Required with detailed Request and Response structure**
