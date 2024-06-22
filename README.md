# Nest
import { Injectable } from '@angular/core';
import { HttpClient } from '@angular/common/http';
import { Observable } from 'rxjs';

@Injectable({
  providedIn: 'root'
})
export class UserService {
  private apiUrl = 'http://your-api-url.com/api'; // Replace with your API URL

  constructor(private http: HttpClient) { }

  getUser(userId: number): Observable<any> {
    return this.http.get(`${this.apiUrl}/users/${userId}`);
  }

  getFollowers(userId: number): Observable<any> {
    return this.http.get(`${this.apiUrl}/users/${userId}/followers`);
  }

  getFollowing(userId: number): Observable<any> {
    return this.http.get(`${this.apiUrl}/users/${userId}/following`);
  }
}




import { Injectable } from '@angular/core';
import { HttpClient } from '@angular/common/http';
import { Observable } from 'rxjs';

@Injectable({
  providedIn: 'root'
})
export class PostService {
  private apiUrl = 'http://your-api-url.com/api'; // Replace with your API URL

  constructor(private http: HttpClient) { }

  getPosts(userId: number): Observable<any> {
    return this.http.get(`${this.apiUrl}/users/${userId}/posts`);
  }

  createPost(postData: any): Observable<any> {
    return this.http.post(`${this.apiUrl}/posts`, postData);
  }
}


<div class="profile-header">
  <h1>{{ user?.username }}</h1>
  <button mat-button (click)="follow()">Follow</button>
  <div class="profile-stats">
    <button mat-button>{{ followers.length }} Followers</button>
    <button mat-button>{{ following.length }} Following</button>
  </div>
</div>

<ng-container *ngIf="posts.length > 0; else noPosts">
  <app-post-grid [posts]="posts"></app-post-grid>
</ng-container>

<ng-template #noPosts>
  <button mat-raised-button color="primary" (click)="createPost()">Create New Post</button>
</ng-template>




import { Component, OnInit } from '@angular/core';
import { UserService } from '../../services/user.service';
import { PostService } from '../../services/post.service';
import { ActivatedRoute } from '@angular/router';

@Component({
  selector: 'app-user-profile',
  templateUrl: './user-profile.component.html',
  styleUrls: ['./user-profile.component.css']
})
export class UserProfileComponent implements OnInit {
  user: any;
  followers: any[] = [];
  following: any[] = [];
  posts: any[] = [];

  constructor(
    private userService: UserService,
    private postService: PostService,
    private route: ActivatedRoute
  ) { }

  ngOnInit(): void {
    const userId = this.route.snapshot.params['id'];
    this.loadUser(userId);
    this.loadFollowers(userId);
    this.loadFollowing(userId);
    this.loadPosts(userId);
  }

  loadUser(userId: number): void {
    this.userService.getUser(userId).subscribe(user => this.user = user);
  }

  loadFollowers(userId: number): void {
    this.userService.getFollowers(userId).subscribe(followers => this.followers = followers);
  }

  loadFollowing(userId: number): void {
    this.userService.getFollowing(userId).subscribe(following => this.following = following);
  }

  loadPosts(userId: number): void {
    this.postService.getPosts(userId).subscribe(posts => this.posts = posts);
  }

  follow(): void {
    // Implement follow functionality here
  }

  createPost(): void {
    // Implement post creation functionality here
  }
}




<div class="post-grid">
  <div *ngFor="let post of posts" class="post">
    <img [src]="post.imageUrl" alt="Post Image">
  </div>
</div>



import { Component, Input, OnInit } from '@angular/core';

@Component({
  selector: 'app-post-grid',
  templateUrl: './post-grid.component.html',
  styleUrls: ['./post-grid.component.css']
})
export class PostGridComponent implements OnInit {
  @Input() posts: any[] = [];

  constructor() { }

  ngOnInit(): void { }
}



.profile-header {
  display: flex;
  flex-direction: column;
  align-items: center;
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
import { HttpClientModule } from '@angular/common/http';
import { MatButtonModule } from '@angular/material/button';
import { MatCardModule } from '@angular/material/card';

import { AppComponent } from './app.component';
import { UserProfileComponent } from './components/user-profile/user-profile.component';
import { PostGridComponent } from './components/post-grid/post-grid.component';

@NgModule({
  declarations: [
    AppComponent,
    UserProfileComponent,
    PostGridComponent
  ],
  imports: [
    BrowserModule,
    BrowserAnimationsModule,
    HttpClientModule,
    MatButtonModule,
    MatCardModule
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }




import { NgModule } from '@angular/core';
import { RouterModule, Routes } from '@angular/router';
import { UserProfileComponent } from './components/user-profile/user-profile.component';

const routes: Routes = [
  { path: 'profile/:id', component: UserProfileComponent },
  { path: '', redirectTo: '/profile/1', pathMatch: 'full' } // Default route for testing
];

@NgModule({
  imports: [RouterModule.forRoot(routes)],
  exports: [RouterModule]
})
export class AppRoutingModule { }
