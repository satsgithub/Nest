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

