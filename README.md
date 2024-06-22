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

