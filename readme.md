# Visualize API responses in POSTMAN
 [link](https://learning.getpostman.com/docs/postman/sending_api_requests/visualizer/)  

# 1. Table 
## Steps
- using GET method find the list of all todos

```
https://jsonplaceholder.typicode.com/todos
```
The responce is 
```
[
  {
    "userId": 1,
    "id": 1,
    "title": "delectus aut autem",
    "completed": false
  },
  {
    "userId": 1,
    "id": 2,
    "title": "quis ut nam facilis et officia qui",
    "completed": false
  },
  {
    "userId": 1,
    "id": 3,
    "title": "fugiat veniam minus",
    "completed": false
  },
]
```
- add the code snippet in Tests Tab

```javascript
var template = `
    <table>
        <tr>
            <th>userid</th>
            <th>id</th>
            <th>title</th>
            <th>Completed</th>
        </tr>

        {{#each response}}
            <tr>
                <td>{{userId}}</td>
                <td>{{id}}</td>
                <td>{{title}}</td>
                <td>{{completed}}</td>
            </tr>
        {{/each}}
    </table>
`;

// Set visualizer
pm.visualizer.set(template, {
    // Pass the response body parsed as JSON as `data`
    response: pm.response.json()
});
```
- go to Visualizer tab
```
responce -> body -> visualizer tab
```
# 2. CHART [chartjs](https://www.chartjs.org/docs/latest/getting-started/)   


## Steps
- using GET method find the list of all todos

```
hhttps://reqres.in/api/users
```
The responce is 
```
{
    "page": 1,
    "per_page": 6,
    "total": 12,
    "total_pages": 2,
    "data": [
        {
            "id": 1,
            "email": "george.bluth@reqres.in",
            "first_name": "George",
            "last_name": "Bluth",
            "avatar": "https://s3.amazonaws.com/uifaces/faces/twitter/calebogden/128.jpg"
        },
        {
            "id": 2,
            "email": "janet.weaver@reqres.in",
            "first_name": "Janet",
            "last_name": "Weaver",
            "avatar": "https://s3.amazonaws.com/uifaces/faces/twitter/josephstein/128.jpg"
        },
        {
            "id": 3,
            "email": "emma.wong@reqres.in",
            "first_name": "Emma",
            "last_name": "Wong",
            "avatar": "https://s3.amazonaws.com/uifaces/faces/twitter/olegpogodaev/128.jpg"
        },
        {
            "id": 4,
            "email": "eve.holt@reqres.in",
            "first_name": "Eve",
            "last_name": "Holt",
            "avatar": "https://s3.amazonaws.com/uifaces/faces/twitter/marcoramires/128.jpg"
        },
        {
            "id": 5,
            "email": "charles.morris@reqres.in",
            "first_name": "Charles",
            "last_name": "Morris",
            "avatar": "https://s3.amazonaws.com/uifaces/faces/twitter/stephenmoon/128.jpg"
        },
        {
            "id": 6,
            "email": "tracey.ramos@reqres.in",
            "first_name": "Tracey",
            "last_name": "Ramos",
            "avatar": "https://s3.amazonaws.com/uifaces/faces/twitter/bigmancho/128.jpg"
        }
    ]
}
```
- add the code snippet in Tests Tab

```javascript
var template = `


<canvas id="myChart"></canvas>

<script src="https://cdn.jsdelivr.net/npm/chart.js@2.8.0"></script>
<script>
var ctx = document.getElementById('myChart').getContext('2d');
var chart = new Chart(ctx, {
    // The type of chart we want to create
    type: 'line',

    // The data for our dataset
    data: {
        labels: ['January', 'February', 'March', 'April', 'May', 'June', 'July'],
        datasets: [{
            label: 'My First dataset',
            backgroundColor: 'rgb(255, 99, 132)',
            borderColor: 'rgb(255, 99, 132)',
            data: [0, 10, 5, 2, 20, 30, 45] // This is going to remove
        }]
    },

    // Configuration options go here
    // options: {}
});

pm.getData(function(err,value){
  chart.data.datasets[0].data= value.response
   chart.update();
})

</script>
`







let response = pm.response.json();

// Set visualizer
pm.visualizer.set(template, {
    // Pass the response body parsed as JSON as `data`
    response: response.data.map(v=> v.id)
});
```
- go to Visualizer tab
```
responce -> body -> visualizer tab
```