For non-referenced credit try to modify the "credit trasaction" function to this:
Credit goes to Corey Huinker.
```
 function credit_transaction($origid,$acct = '', $expdate = '',$amt = '') { 
 
if ((strlen($origid) < 3) && ($origid != 'NR')) { 
$this->set_errors('OrigID not valid'); 
return; 
} 
 
// build hash 
$tempstr = $card_number . $amount . date('YmdGis') . "2"; 
$request_id = md5($tempstr); 
 
// body 
$plist = 'USER=' . $this->user . '&'; 
$plist .= 'VENDOR=' . $this->vendor . '&'; 
$plist .= 'PARTNER=' . $this->partner . '&'; 
$plist .= 'PWD=' . $this->password . '&'; 
$plist .= 'TENDER=' . 'C' . '&'; // C = credit card, P = PayPal 
$plist .= 'TRXTYPE=' . 'C' . '&'; // S = Sale transaction, A = Authorisation, C = Credit, D = Delayed Capture, V = Void 
 
if ($origid == 'NR') { 
// non-referenced credit 
$plist .= 'ACCT=' . $acct . '&'; 
$plist .= 'EXPDATE=' . $expdate . '&'; 
$plist .= 'AMT=' . $amt . '&'; 
}else { 
$plist .= 'ORIGID=' . $origid . '&'; // ORIGID to the PNREF value returned from the original transaction 
} 

```