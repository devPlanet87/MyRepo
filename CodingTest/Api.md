#### API #1 Create API to insert books

#### API #2 Create API to insert authors

#### API #3 Create API to Get book by author

##### Controller:

###### BookController:
```cs
public class BookController : ControllerBase
{
  private readonly IBookService _svc;
  private readonly ILogger _logger;
  BookController(IBookService svc, ILogger logger)
  {
    _svc = svc;
    _logger = logger;
  }

  [HttpPost]
  [Route("Book")]
  public async Task<IActionResult> Book([FromBody] BookModel model)
  {
      try
      {
          return Ok(_svc.AddBook(model));
      }
      catch(Exception ex)
      {
          logger.LogError(ex);
          return StatusCode(500, ex.Message);
      }
  }
}
```
###### AuthorController:
```cs
public class AuthorController : ControllerBase
{
  private readonly IAuthorService _svc;
  private readonly ILogger _logger;
  AuthorController(IAuthorService svc, ILogger logger)
  {
    _svc = svc;
    _logger = logger;
  }

  [HttpPost]
  [Route("Author")]
  public async Task<IActionResult > Author([FromBody] AuthorModel model)
  {
      try
      {
          return Ok(_svc.AddAuthor(model));
      }
      catch(Exception ex)
      {
          logger.LogError(ex);
          return StatusCode(500, ex.Message);
      }
  }
}
```
