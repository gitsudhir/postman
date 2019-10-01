# Visualize API responses in POSTMAN
 [link](https://learning.getpostman.com/docs/postman/sending_api_requests/visualizer/)

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
