import { Component } from '@angular/core';
import {environment} from "../../environments/environment";
import { HttpClient } from '@angular/common/http';

@Component({
  selector: 'app-image-nasa',
  templateUrl: './image-nasa.component.html',
  styleUrls: ['./image-nasa.component.scss']
})



export class ImageNasaComponent {

  title!: string;
  description!: string;
  date!: Date;
  imageUrls!: string[];
  apiKey = environment.apiKey;

  constructor(private http: HttpClient) {
  }

  ngOnInit() {
    this.imageUrls = [];

    this.http.get<any>("https://api.nasa.gov/planetary/apod?api_key="  + this.apiKey + "&count=" + 10 ).subscribe(data => {
      for (let i in data) {
        let image = data[i].url;
        this.imageUrls.push(image);
      }
    });


    this.title = "d";
    this.description = "d";
    this.date = new Date();
  }
}
