# practice
mysql

Q1: Replace the prefix for the matching prefix in values of n_token columnn in login_data table. 
login_data

n_token 
lib_asdhfo0das9lib_fdasklfjd0f8asdf
Replace lib_ prefix from to xyz-



UPDATE login_data
SET n_token = concat('xyz-', substring('lib_asdhfo0das9lib_fdasklfjd0f8asdf', 5))
WHERE n_token LIKE 'lib_%';



Q2: Find recursive child for the given parent using mysql query?
Users

id      name        parent_id
1       Manish      0
2       Manish2      1
3       Manish3      2
4       Manish4      2


CREATE TABLE `users` (
  `id` int(11) DEFAULT NULL,
  `name` varchar(20) DEFAULT NULL,
  `parent_id` int(11) DEFAULT NULL
);

insert into `users` (`id`, `name`, `parent_id`) values('1','Manish','0');
insert into `users` (`id`, `name`, `parent_id`) values('2','Manish2','1');
insert into `users` (`id`, `name`, `parent_id`) values('3','Manish3','2');
insert into `users` (`id`, `name`, `parent_id`) values('4','Manish4','3');
insert into `users` (`id`, `name`, `parent_id`) values('5','Manish5','4');
insert into `users` (`id`, `name`, `parent_id`) values('6','Manish6','5');
insert into `users` (`id`, `name`, `parent_id`) values('7','Manish7','4');
insert into `users` (`id`, `name`, `parent_id`) values('8','Manish8','1');


select  id,
        name,
        parent_id
from    (select * from users
         order by parent_id, id) as  users,
        (select @var := '2') as init
where   find_in_set(parent_id, @var) > 0
and     @var := concat(@var, ',', id);
