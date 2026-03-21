select first_name, target from salesforce_employees
where target = (
select target
from salesforce_employees
where 1=1
and manager_id=13
limit 1
)
and manager_id=13
;

nothing new here, its just usual rank and filtering