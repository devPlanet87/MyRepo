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
          if(model == null)
          {
            return BadRequest("Invalid model.");
          }

          return Ok(await _svc.CreateBook(model));
      }
      catch(Exception ex)
      {
          _logger.LogError(ex);
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
  public async Task<IActionResult> Author([FromBody] AuthorModel model)
  {
      try
      {
          if(model == null)
          {
            return BadRequest("Invalid model.");
          }

          return Ok(await _svc.CreateAuthor(model));
      }
      catch(Exception ex)
      {
          _logger.LogError(ex);
          return StatusCode(500, ex.Message);
      }
  }
}
```
###### LibraryController:
```cs
public class LibraryController : ControllerBase
{
  private readonly ILibraryService _svc;
  private readonly ILogger _logger;

  LibraryController(ILibraryService svc, ILogger logger)
  {
    _svc = svc;
    _logger = logger;
  }

  [HttpGet]
  [Route("BooksByAuthor")]
  public async Task<IEnumerable<Book>> BookDetails(int authorId)
  {
      try
      {
          if(authorId == 0)
          {
            return BadRequest("Invalid authorId.");
          }

          return Ok(await _svc.GetBooksByAuthor(authorId));
      }
      catch(Exception ex)
      {
          _logger.LogError(ex);
          return StatusCode(500, ex.Message);
      }
  }
}
```
