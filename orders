function getProductOrders() {

  //URL of Domain ending in '/'
  var apiHost = 'https://example.com/'
  
  
  var headers = {"Authorization" : "Basic " + Utilities.base64Encode('CONSUMER_KEY'+':'+'SECRET_KEY')
  //"Authorization" : "Basic " + Utilities.base64Encode(PropertiesService.getDocumentProperties().getProperty('consumer_key')+':'+PropertiesService.getDocumentProperties().getProperty('consumer_secret'))
  //if you set keys as env variables - google it
    }; 
  
  var options = {
      'method': 'get',
      'headers': headers,
      "contentType" : "application/json",
      'muteHttpExceptions': false
    }
  
  var url = apiHost + 'wp-json/wc/v3/orders?';
  //per_page='+per_page+'&amp;offset='+offset;
  
  var getUrl = UrlFetchApp.fetch(url,options);
  
  var response = JSON.parse(getUrl);
  
  var page = [];
  
  for (i =0;i<response.length;i++){
  
      page.push([
        response[i].date_paid,
        response[i].id,
        response[i].status,
        response[i].billing.postcode,
        response[i].line_items[0].name,
        response[i].line_items[0].quantity,
        response[i].line_items[0].sku,
        response[i].line_items[0].price
        
        ])
        
        for (j=1; j<response[i].line_items.length; j++){
          page.push([
            response[i].date_paid,
            response[i].id,
            response[i].status,
            response[i].billing.postcode,
            response[i].line_items[j].name,
            response[i].line_items[j].quantity,
            response[i].line_items[j].sku,
            response[i].line_items[j].price,
    
          ])
        
        }
      
    };
    
    var getstartingRow = 'A2';
    
    var getendingRow = page.length;
    
    var rangeSize = 1+getendingRow;
    
    //must change when expanding results
    var pageRange = 'A2:H'+rangeSize;
    
    var ss = SpreadsheetApp.getActive().getSheetByName('Product.LCA');
    
    ss.getRange(pageRange).clearContent().setValues(page);
    
}
