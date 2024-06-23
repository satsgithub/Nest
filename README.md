<div class="profile-header">
  <h1>{{ user.username }}</h1>
  <button mat-button (click)="follow()">Follow</button>
  <div class="profile-stats">
    <button mat-button>{{ followers.length }} Followers</button>
    <button mat-button>{{ following.length }} Following</button>
  </div>
</div>

<ng-container *ngIf="posts.length > 0; else noPosts">
  <div class="post-grid">
    <div *ngFor="let post of posts" class="post">
      <img [src]="post.imageUrl" alt="Post Image">
    </div>
  </div>
</ng-container>

<ng-template #noPosts>
  <button mat-raised-button color="primary" (click)="createPost()">Create New Post</button>
</ng-template>



import { Component, OnInit } from '@angular/core';

@Component({
  selector: 'app-user-profile',
  templateUrl: './user-profile.component.html',
  styleUrls: ['./user-profile.component.css']
})
export class UserProfileComponent implements OnInit {
  user: any = {
    username: 'john_doe'
  };
  followers: any[] = [
    { id: 1, name: 'Follower 1' },
    { id: 2, name: 'Follower 2' }
  ];
  following: any[] = [
    { id: 1, name: 'Following 1' },
    { id: 2, name: 'Following 2' }
  ];
  posts: any[] = [
    { id: 1, imageUrl: 'https://via.placeholder.com/150' },
    { id: 2, imageUrl: 'https://via.placeholder.com/150' }
  ];

  constructor() { }

  ngOnInit(): void { }

  follow(): void {
    // Implement follow functionality here
  }





  ===========================

  ngOnInit(): void {
    this.route.paramMap.subscribe(params => {
      this.username = params.get('username') || 'defaultUser';
      this.loadUserProfile();
    });
  }

  loadUserProfile(): void {
    this.apiService.getUserProfile(this.username).subscribe(
      data => this.userProfile = data,
      error => console.error('Error fetching user profile', error)
    );
  }

  createPost(): void {
    const newPost = {
      postByUser: this.username,
      caption: 'New Post',
      location: 'Location',
      postUrls: [
        { mediaType: 'image', mediaUrl: 'http://example.com/image.jpg' }
      ]
    };

    this.apiService.createPost(newPost).subscribe(
      response => {
        console.log('Post created successfully', response);
        this.loadUserProfile(); // Refresh the user profile to reflect the new post
      },
      error => console.error('Error creating post', error)
    );
  }
}

  createPost(): void {
    // Implement post creation functionality here
  }
}



.profile-header {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-bottom: 20px;
}

.profile-stats {
  display: flex;
  gap: 10px;
}

.post-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(150px, 1fr));
  gap: 10px;
}

.post {
  width: 150px;
  height: 150px;
  overflow: hidden;
}

.post img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}



import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { BrowserAnimationsModule } from '@angular/platform-browser/animations';
import { MatButtonModule } from '@angular/material/button';
import { MatCardModule } from '@angular/material/card';

import { AppComponent } from './app.component';
import { UserProfileComponent } from './components/user-profile/user-profile.component';
import { AppRoutingModule } from './app-routing.module'; // Import the routing module

@NgModule({
  declarations: [
    AppComponent,
    UserProfileComponent
  ],
  imports: [
    BrowserModule,
    BrowserAnimationsModule,
    MatButtonModule,
    MatCardModule,
    AppRoutingModule
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }




import { NgModule } from '@angular/core';
import { RouterModule, Routes } from '@angular/router';
import { UserProfileComponent } from './components/user-profile/user-profile.component';

const routes: Routes = [
  { path: 'profile', component: UserProfileComponent },
  { path: '', redirectTo: '/profile', pathMatch: 'full' } // Default route for testing
];

@NgModule({
  imports: [RouterModule.forRoot(routes)],
  exports: [RouterModule]
})
export class AppRoutingModule { }




<div class="profile-container">
  <div class="profile-header">
    <div class="profile-avatar">
      <img [src]="user.avatarUrl" alt="{{ user.username }}">
    </div>
    <div class="profile-info">
      <div class="profile-username">
        <h2>{{ user.username }}</h2>
        <button mat-raised-button color="primary" (click)="follow()">Follow</button>
      </div>
      <div class="profile-stats">
        <span>{{ posts.length }} posts</span>
        <span>{{ followers.length }} followers</span>
        <span>{{ following.length }} following</span>
      </div>
      <div class="profile-bio">
        <p>{{ user.bio }}</p>
      </div>
    </div>
  </div>

  <ng-container *ngIf="posts.length > 0; else noPosts">
    <div class="post-grid">
      <div *ngFor="let post of posts" class="post">
        <img [src]="post.imageUrl" alt="Post Image">
      </div>
    </div>
  </ng-container>

  <ng-template #noPosts>
    <div class="no-posts">
      <p>No posts yet.</p>
      <button mat-raised-button color="primary" (click)="createPost()">Create New Post</button>
    </div>
  </ng-template>
</div>






.profile-container {
  max-width: 935px;
  margin: 0 auto;
  padding: 20px;
}

.profile-header {
  display: flex;
  align-items: center;
  margin-bottom: 30px;
}

.profile-avatar {
  flex: 0 0 150px;
  margin-right: 30px;
}

.profile-avatar img {
  width: 150px;
  height: 150px;
  border-radius: 50%;
}

.profile-info {
  flex: 1;
}

.profile-username {
  display: flex;
  align-items: center;
  margin-bottom: 20px;
}

.profile-username h2 {
  margin: 0;
  margin-right: 20px;
  font-size: 28px;
}

.profile-stats {
  display: flex;
  gap: 20px;
  margin-bottom: 20px;
}

.profile-stats span {
  font-weight: bold;
}

.profile-bio {
  font-size: 16px;
}

.post-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(293px, 1fr));
  gap: 28px;
}

.post {
  position: relative;
  width: 100%;
  padding-top: 100%; /* 1:1 Aspect Ratio */
  overflow: hidden;
}

.post img {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.no-posts {
  text-align: center;
  margin-top: 20px;
}






import { Component, OnInit } from '@angular/core';
import { ActivatedRoute } from '@angular/router';

@Component({
  selector: 'app-user-profile',
  templateUrl: './user-profile.component.html',
  styleUrls: ['./user-profile.component.css']
})
export class UserProfileComponent implements OnInit {
  userId: string; // Assuming you have userId coming from route params
  user: any = {
    username: '',
    avatarUrl: '',
    bio: ''
  };
  followers: any[] = [];
  following: any[] = [];
  posts: any[] = [];

  constructor(private route: ActivatedRoute) { }

  ngOnInit(): void {
    // Retrieve userId from route parameters
    this.route.params.subscribe(params => {
      this.userId = params['id']; // Adjust 'id' based on your actual route parameter
      // Load user profile data based on userId (simulated)
      this.fetchUserProfile(this.userId);
      this.fetchUserPosts(this.userId);
    });
  }

  fetchUserProfile(userId: string): void {
    // Simulate fetching user profile data based on userId
    // Replace with actual API call to fetch user data
    // Mock data for demonstration
    setTimeout(() => {
      this.user = {
        username: 'john_doe',
        avatarUrl: 'https://via.placeholder.com/150',
        bio: 'This is a short bio about John Doe.'
      };
      this.followers = [
        { id: 1, name: 'Follower 1' },
        { id: 2, name: 'Follower 2' }
      ];
      this.following = [
        { id: 1, name: 'Following 1' },
        { id: 2, name: 'Following 2' }
      ];
    }, 1000); // Simulate delay of 1 second (1000 ms)
  }

  fetchUserPosts(userId: string): void {
    // Simulate fetching user posts based on userId
    // Replace with actual API call to fetch user posts
    // Mock data for demonstration
    setTimeout(() => {
      this.posts = [
        { id: 1, imageUrl: 'https://via.placeholder.com/293', description: 'First post' },
        { id: 2, imageUrl: 'https://via.placeholder.com/293', description: 'Second post' }
      ];
    }, 1500); // Simulate delay of 1.5 seconds (1500 ms)
  }

  follow(): void {
    // Simulate following user functionality
    // Replace with actual logic to follow user
    console.log('Follow button clicked');
    // Example: Add a new follower
    const newFollower = { id: this.followers.length + 1, name: `New Follower ${this.followers.length + 1}` };
    this.followers.push(newFollower);
  }

  createPost(): void {
    // Simulate creating a new post functionality
    // Replace with actual logic to create new post
    console.log('Create Post button clicked');
    // Example: Add a new post
    const newPost = {
      id: this.posts.length + 1,
      imageUrl: 'https://via.placeholder.com/293',
      description: 'New Post'
    };
    this.posts.unshift(newPost); // Add new post to the beginning of the array
  }
}









==============================================================================================================================



-- Om
 
create database SocialMedia
 
use SocialMedia
 
create table Gender
(
id int primary key,
name nvarchar(25) not null,
)
 
create table AccountType
(
id int primary key,
AccType nvarchar(20) not null
)
 
create table Users
(
UserName nvarchar(100) primary key,
Name nvarchar(50) not null,
Email nvarchar(50) not null unique,
ContactNumber bigint NOT NULL Unique CHECK  ((len(CONVERT(varchar,ContactNumber))=(10))), 
DOB date not null,
Location nvarchar(50) not null,
Bio nvarchar(300),
ProfilePicURL nvarchar(500),
GenderId int references Gender(id) not null,
AccountTypeID int references AccountType(id) not null,
CreatedAt date default GetDate(),
UpdatedAt date default GetDate(),
 
LastSeen date default GetDate(),
isActive BIT default 0,
 
isDeactivated BIT default 0,
 
isBlocked BIT default 0,
isReported BIT default 0,
);
 
create table Circle
(
UserName nvarchar(100) references Users(UserName),
Following nvarchar(100) references Users(UserName),
FollowedDate date default GETDATE(),
CONSTRAINT CKForCircle PRIMARY KEY(UserName, Following)
)
 
CREATE TABLE Tags
(
PostID int references Posts(ID),
TaggedUser NVARCHAR(100) references Users(UserName)
Constraint CkForTags Primary KEY(PostID, TaggedUser)
)
 
CREATE TABLE Posts
(
ID INT PRIMARY KEY,
PostByUser NVARCHAR(100) references Users(UserName),
Caption NVARCHAR(4000),
Location NVARCHAR(50),
PostedAt Date default GETDATE()
)
 
Create Table PostURls
(
ID int Primary Key,
PostID INT references Posts(ID),
MediaType NVARCHAR(20) NOT NULL,   ---images, videos
MediaUrl NVARCHAR(4000) NOT NULL,
)
 
CREATE TABLE Likes
(
PostID int references Posts(ID),
UserName nvarchar(100) references Users(UserName),
LikedAt date default GETDATE(),
CONSTRAINT CKForLikes Primary Key(PostID, UserName)
)
 
CREATE TABLE Comments
(
ID int Primary KEY,
PostID int references Posts(ID),
UserName nvarchar(100) references Users(UserName),
Comment nvarchar(500) not null,
CommentedAt date default GETDATE(),
)
 
Create Table ReportType
(
ID int primary key,
Category nvarchar(100) not null
)
 
Create Table Report
(
ID int primary key,
PostID int References Posts(ID),
Reporter nvarchar(100) references Users(UserName),
ReportTypeID int references ReportType(ID),
ReportDate date default GETDATE(),
Message nvarchar(500),
isResolved BIT default 0
)
 
Create Table BlockedUsers
(
UserName nvarchar(100) references Users(UserName),
BlockedUser nvarchar(100) references Users(UserName),
BlockDate date default GETDATE(),
CONSTRAINT CkForBlock PRIMARY KEY(UserName, BlockedUser)
)
 
Create Table SavePost
(
PostID int references Posts(ID),
UserName nvarchar(100) references Users(UserName),
SaveDate date default GETDATE(),
CONSTRAINT CkForSave PRIMARY KEY(PostID, UserName)
)
 
Create Table Story
(
ID int primary key,
UserName nvarchar(100) references Users(UserName),
MediaType NVARCHAR(20) NOT NULL,   ---images, videos
MediaUrl NVARCHAR(4000) NOT NULL,
React nvarchar(5),
AddDate date default GETDATE()
)
 
Create Table Chat
(
conversationID int not null,
sender nvarchar(100) references Users(UserName),
reciever nvarchar(100) references Users(UserName),
postId int references Posts(ID),
messageId int primary key,
message nvarchar(100) not null,
attachmenturl nvarchar(4000),
isDeleted bit default 0,
isUpdated bit default 0,
sentDate datetime default GETDATE()
)
 
 
CREATE TABLE Promotion
(
ID int primary key,
LocationPreference nvarchar(50),
PlaceDate  Date default GETDATE(),
PostID int foreign key references Posts(ID),
ReachAndPriceID int references ReachAndPrice(ID),
isActive BIT default 0
)
 
create table ReachAndPrice
(
ID int primary key,
Reach int,
Price float
)
 
-- 18
 
create table PromotionReach
(
PromotionID int references Promotion(ID),
ViewedUser nvarchar(100) references Users(UserName),
)
 
CREATE TABLE Admin
( 
UserName int primary key,
Name nvarchar(30),
EmailId nvarchar(100),
ContactNumber bigint NOT NULL CHECK  ((len(CONVERT(varchar,ContactNumber))=(10)))
)



==================================================================================================================================================






using Microsoft.AspNetCore.Mvc;
using Microsoft.EntityFrameworkCore;
using System.Linq;
using System.Threading.Tasks;

[Route("api/[controller]")]
[ApiController]
public class UserProfileController : ControllerBase
{
    private readonly SocialMediaContext _context;

    public UserProfileController(SocialMediaContext context)
    {
        _context = context;
    }

    [HttpGet("{username}")]
    public async Task<IActionResult> GetUserProfile(string username)
    {
        var user = await _context.Users
            .Where(u => u.UserName == username)
            .Select(u => new
            {
                u.UserName,
                u.Name,
                u.ProfilePicUrl,
                u.Bio,
                u.Location,
                FollowersCount = _context.Circles.Count(c => c.Following == u.UserName),
                FollowingCount = _context.Circles.Count(c => c.UserName == u.UserName),
                Posts = _context.Posts.Where(p => p.PostByUser == u.UserName)
                                      .Select(p => new { p.ID, p.Caption, p.PostedAt, p.Location, p.PostUrls })
                                      .ToList()
            })
            .FirstOrDefaultAsync();

        if (user == null)
        {
            return NotFound();
        }

        return Ok(user);
    }

    [HttpPost("createPost")]
    public async Task<IActionResult> CreatePost([FromBody] Post newPost)
    {
        _context.Posts.Add(newPost);
        await _context.SaveChangesAsync();
        return CreatedAtAction(nameof(GetUserProfile), new { username = newPost.PostByUser }, newPost);
    }
}



=====================================

CREATE TRIGGER InsertPostUrls
ON Posts
AFTER INSERT
AS
BEGIN
    DECLARE @PostID INT
    SELECT @PostID = ID FROM INSERTED

    -- Example: Add media URLs (This part needs to be adapted based on your actual use case)
    INSERT INTO PostUrls (PostID, MediaType, MediaUrl)
    VALUES (@PostID, 'image', 'http://example.com/image1.jpg'),
           (@PostID, 'video', 'http://example.com/video1.mp4');
END;




==============


using Microsoft.AspNetCore.Mvc;
using Microsoft.EntityFrameworkCore;
using System.Linq;
using System.Threading.Tasks;

[Route("api/[controller]")]
[ApiController]
public class UserProfileController : ControllerBase
{
    private readonly SocialMediaContext _context;

    public UserProfileController(SocialMediaContext context)
    {
        _context = context;
    }

    [HttpGet("{username}")]
    public async Task<IActionResult> GetUserProfile(string username)
    {
        var user = await _context.Users
            .Where(u => u.UserName == username)
            .Select(u => new
            {
                u.UserName,
                u.Name,
                u.ProfilePicUrl,
                u.Bio,
                u.Location,
                FollowersCount = _context.Circles.Count(c => c.Following == u.UserName),
                FollowingCount = _context.Circles.Count(c => c.UserName == u.UserName),
                Posts = _context.Posts
                                .Where(p => p.PostByUser == u.UserName)
                                .Select(p => new
                                {
                                    p.ID,
                                    p.Caption,
                                    p.PostedAt,
                                    p.Location,
                                    PostUrls = _context.PostUrls
                                                       .Where(url => url.PostID == p.ID)
                                                       .Select(url => new { url.MediaType, url.MediaUrl })
                                                       .ToList()
                                })
                                .ToList()
            })
            .FirstOrDefaultAsync();

        if (user == null)
        {
            return NotFound();
        }

        return Ok(user);
    }

    [HttpPost("createPost")]
    public async Task<IActionResult> CreatePost([FromBody] Post newPost)
    {
        if (newPost == null || newPost.PostUrls == null || !newPost.PostUrls.Any())
        {
            return BadRequest();
        }

        _context.Posts.Add(newPost);
        await _context.SaveChangesAsync();

        // Manually add PostUrls since the trigger won't have them
        foreach (var url in newPost.PostUrls)
        {
            url.PostID = newPost.ID;
            _context.PostUrls.Add(url);
        }
        await _context.SaveChangesAsync();

        return CreatedAtAction(nameof(GetUserProfile), new { username = newPost.PostByUser }, newPost);
    }
}

============================================================



        [HttpGet("{username}")]
        
        public async Task<IActionResult> GetUserProfile(string username)
        {
            var user = await _context.Users
                .Where(u => u.UserName == username)
                .Select(u => new
                {
                    u.UserName,
                    u.Name,
                    u.ProfilePicUrl,
                    u.Bio,
                    u.Location,
                    FollowersCount = _context.Circles.Count(c => c.Following == u.UserName),
                    FollowingCount = _context.Circles.Count(c => c.UserName == u.UserName),
                    Posts = _context.Posts.Where(p => p.PostByUser == u.UserName)
                                          .Select(p => new { p.Id, p.Caption, p.PostedAt, p.Location, p.PostUrls })
                                          .ToList()
                })
                .FirstOrDefaultAsync();

            if (user == null)
            {
                return NotFound();
            }

            return Ok(user);
        }

        [HttpPost("createPost")]

        public async Task<IActionResult> CreatePost([FromBody] Post newPost)
        {
            int i = 2;
            _context.Posts.Add(newPost);


            PostUrl objPostUrl = new PostUrl();
            objPostUrl.Id = i++;
            objPostUrl.PostId = newPost.Id;
            objPostUrl.MediaType = "image";
            objPostUrl.MediaUrl = "C:\\Users\\satyasingh\\source\\repos\\Project_img.jpg";
            _context.PostUrls.Add(objPostUrl);
            await _context.SaveChangesAsync();



            await _context.SaveChangesAsync();
            return CreatedAtAction(nameof(GetUserProfile), new { username = newPost.PostByUser }, newPost);
        }

=====================


import { Injectable } from '@angular/core';
import { HttpClient } from '@angular/common/http';
import { Observable } from 'rxjs';

@Injectable({
  providedIn: 'root'
})
export class ApiService {
  private apiUrl = 'https://localhost:5001/api';

  constructor(private http: HttpClient) { }

  getUserProfile(username: string): Observable<any> {
    return this.http.get(`${this.apiUrl}/UserProfile/${username}`);
  }

  createPost(post: any): Observable<any> {
    return this.http.post(`${this.apiUrl}/UserProfile/createPost`, post);
  }
}

==============


import { Component, OnInit } from '@angular/core';
import { ApiService } from '../api.service';
import { ActivatedRoute } from '@angular/router';

@Component({
  selector: 'app-user-profile',
  templateUrl: './user-profile.component.html',
  styleUrls: ['./user-profile.component.css']
})
export class UserProfileComponent implements OnInit {
  userProfile: any;
  username: string;

  constructor(private apiService: ApiService, private route: ActivatedRoute) { }

  ngOnInit(): void {
    this.route.paramMap.subscribe(params => {
      this.username = params.get('username') || 'defaultUser';
      this.loadUserProfile();
    });
  }

  loadUserProfile(): void {
    this.apiService.getUserProfile(this.username).subscribe(
      data => this.userProfile = data,
      error => console.error('Error fetching user profile', error)
    );
  }

  createPost(): void {
    const newPost = {
      postByUser: this.username,
      caption: 'New Post',
      location: 'Location',
      postUrls: [
        { mediaType: 'image', mediaUrl: 'http://example.com/image.jpg' }
      ]
    };

    this.apiService.createPost(newPost).subscribe(
      response => {
        console.log('Post created successfully', response);
        this.loadUserProfile(); // Refresh the user profile to reflect the new post
      },
      error => console.error('Error creating post', error)
    );
  }
}







khgccjjk





using Microsoft.AspNetCore.Mvc;
using Microsoft.EntityFrameworkCore;
using System.Linq;
using System.Threading.Tasks;

[Route("api/[controller]")]
[ApiController]
public class UserProfileController : ControllerBase
{
    private readonly YourDbContext _context;

    public UserProfileController(YourDbContext context)
    {
        _context = context;
    }

    // Other existing methods...

    [HttpGet("{username}/followers")]
    public async Task<IActionResult> GetFollowers(string username)
    {
        var followers = await _context.Circle
            .Where(c => c.Following == username)
            .Select(c => new 
            {
                c.UserName,
                FollowerDetails = _context.Users
                    .Where(u => u.UserName == c.UserName)
                    .Select(u => new 
                    {
                        u.UserName,
                        u.Name,
                        u.ProfilePicURL
                    })
                    .FirstOrDefault()
            })
            .ToListAsync();

        if (followers == null || !followers.Any())
        {
            return NotFound();
        }

        return Ok(followers);
    }
}

=====================================================================================
[HttpPost("createPost")]
public async Task<IActionResult> CreatePost([FromBody] Post newPost)
{
    _context.Posts.Add(newPost);
    await _context.SaveChangesAsync();
                
    return CreatedAtAction(nameof(GetUserProfile), new { username = newPost.PostByUser }, newPost);
}


[HttpPost("createPostURL")]
public async Task<IActionResult> CreatePostURL([FromBody] PostUrl newPostUrl)
{
    _context.PostUrls.Add(newPostUrl);
    await _context.SaveChangesAsync();
    return CreatedAtAction(nameof(GetUserProfile), new { username = newPostUrl.MediaUrl }, newPostUrl);
}







===========

using Microsoft.AspNetCore.Mvc;
using Microsoft.EntityFrameworkCore;
using System.Linq;
using System.Threading.Tasks;

[Route("api/[controller]")]
[ApiController]
public class UserProfileController : ControllerBase
{
    private readonly YourDbContext _context;

    public UserProfileController(YourDbContext context)
    {
        _context = context;
    }

    // Other existing methods...

    [HttpGet("{username}/posts")]
    public async Task<IActionResult> GetUserPosts(string username)
    {
        var posts = await _context.Posts
            .Where(p => p.PostByUser == username)
            .Select(p => new 
            {
                p.Id,
                p.Caption,
                p.Location,
                p.PostedAt,
                PostUrls = _context.PostUrls
                    .Where(pu => pu.PostId == p.Id)
                    .Select(pu => new 
                    {
                        pu.Id,
                        pu.MediaType,
                        pu.MediaUrl
                    })
                    .ToList()
            })
            .ToListAsync();

        if (posts == null || !posts.Any())
        {
            return NotFound();
        }

        return Ok(posts);
    }
}


===================================

import { Injectable } from '@angular/core';
import { HttpClient } from '@angular/common/http';
import { Observable } from 'rxjs';

@Injectable({
  providedIn: 'root'
})


export class ApiService {
  private apiUrl = 'https://localhost:44373/api';
 // https://localhost:44373/api/UserProfile/satya
  constructor(private http: HttpClient) { }

  getUserProfile(username: string): Observable<any> {
    return this.http.get<any>(`https://localhost:44373/api/UserProfile/${username}`);
  }



  // createPost(post: any): Observable<any> {
  //   return this.http.post(`${this.apiUrl}/UserProfile/createPost`, post);
  // }
}










