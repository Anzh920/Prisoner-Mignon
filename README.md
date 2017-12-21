# Prisoner-Mignon
 private void OnMouseDown()     
 {         
   if (render.sprite == null || BoardManager.instance.IsShifting)         
 {             
   return;         
 }         
 if (isSelected)         
 {            
   Deselect();         
 }         
 else         
 {             
   if (previousSelected == null)             
 {                 
   Select();           
 }             
 else           
 {                 
   if (GetAllAdjacentTiles().Contains(previousSelected.gameObject))             
 {                     
   SwapSprite(previousSelected.render);                  
   previousSelected.ClearAllMatches();           
   ClearAllMatches();                     
   previousSelected.Deselect();           
 }           
 else               
 {                  
   previousSelected.GetComponent&lt;Tile>().Deselect();    
   Select();      
  }
 } 
}}   
public void SwapSprite(SpriteRenderer render2)    
{         
  if(render.sprite == render2.sprite)       
   {           
    return;      
   }        
  Sprite tempSprite = render2.sprite;     
  render2.sprite = render.sprite;    
  render.sprite = tempSprite;      
  SFXManager.instance.PlaySFX(Clip.Swap);     
 }      
 private GameObject GetAdjacent(Vector2 castDir)  
 {
  RaycastHit2D hit = Physics2D.Raycast(transform.position, castDir);       
  if (hit.collider != null)       
  {             
    return hit.collider.gameObject;       
  }        
  return null;   
 }      
 private List&lt;GameObject> GetAllAdjacentTiles()     
 {      
  List&lt;GameObject> adjacentTiles = new List&lt;GameObject>();        
  for (int i = 0; i &lt; adjacentDirections.Length; i++)         
   {           
     adjacentTiles.Add(GetAdjacent(adjacentDirections[i]));    
   }        
  return adjacentTiles;    
 }     
 private List&lt;GameObject> FindMatch(Vector2 castDir)     
 {       
  List&lt;GameObject> matchingTiles = new List&lt;GameObject>();   
  RaycastHit2D hit = Physics2D.Raycast(transform.position, castDir);    
  while (hit.collider != null &amp;&amp; hit.collider.GetComponent&lt;SpriteRenderer>().sprite == render.sprite)         
  {             
    matchingTiles.Add(hit.collider.gameObject);      
    hit = Physics2D.Raycast(hit.collider.transform.position, castDir);      
  }        
  return matchingTiles;      
 }
