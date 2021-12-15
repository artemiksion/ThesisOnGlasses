Входные данные:
В начале вводится количество направлений(стаканов), потом для каждого направления количество мест, потом вводится количество абитуриентов, потом начинают вводится сами абитуриенты, вводится их персональный номер, вводится количество приоритетов каждого абитуриента, а потом вводится цифра направления(0 - допустим программная инженерия, 1 - прикладная математика и так далее) и баллы абитуриента для данного направления(количество этих баллов ни на что не влияет, будь их 5(6), для бакалавра или специалитета или 3 для магистров или 2 для аспирантов, главное, чтобы они были переданы в порядке приоритета, типа для бакалавра вначале сумму проверяем, при равенстве 1 предмет, при равенстве 2 предмет и тд).
Потом в сам алгоритм передаётся вектор абитуриентов(который содержит персональные номера студентов, их приоритеты и номер их текущего приоритета, изначально он у всех 0, если по 0 приоритету они не попадают, переменная увеличивается на 1, так сказать отслеживание приоритетов, на котором мы остановились, чтобы каждый раз все приоритеты с начала не смотреть), вектор направлений(который хранит для каждого направления номера абитуриентов, количество номеров абитуриентов не превышает количества мест на направлении).

Суть алгоритма:
Мы начинаем проходить по приоритетам абитуриентов(под приоритетом я подразумеваю направления, которые расставлены по приоритетам зачисления, так как направления у нас - это цифры, то у какого-нибудь абитуриента может быть такая картина приоритетов 0. 5, 1. 3, 2. 9, 3. 2 - первый приоритет - пятое направление, второй приоритет - третье направление и так далее), то есть пытаемся вставить абитуриентов по их первым приоритетам(вставляем по количеству баллов абитуриентов по данному направлению и хранение абитуриентов по направлениям происходит в порядке убывания количества баллов, при вставке мы соответственно сохраняем этот порядок), если какой-то абитуриент не влезает, мы его запоминаем(запоминаем до тех пор, пока у этого абитуриента ещё есть приоритеты, то есть если мы смотрим 3 приоритет абитуриентов, а у данного абитуриента их всего 3 и он по 3 приоритету не проходит, то он просто выкидывается). 
Так мы прошли по первым приоритетам, теперь идём по вторым приоритетам уже не всех абитуриентов, а только тех, кто не попал по своему первому приоритету, дальше если у нас по второму приоритету не получается вставить, то мы так же запоминаем его(и будем смотреть его 3 приоритет), а если у нас получается, тогда мы смотрим, полностью ли заполнено направление, если не полностью, то мы просто вставляем туда абитуриента, а если полностью, тогда мы вставляем абитуриента и выкидываем из этого направления абитуриента с наименьшим количеством баллов(самого последнего) и если мы сейчас проходим по второму приоритету, а абитуриент которого мы выкинули был на своём первом приоритете, то мы увеличиваем текущий приоритет этого абитуриента и рекурсивно вызываем функцию вставки этого выкинутого абитуриента в его текущий приоритет для этого абитуриента (эти вызовы происходят либо до текущего приоритета, то есть сейчас мы смотрим у всех абитуриентов их второй приоритет, значит мы пытаемся его вставить по очереди во все направления соответствующие его приоритетам до второго, либо пока не кончится количество приоритетов у самого студента), и так мы смотрим все приоритеты абитуриентов(если например у всех абитуриентов 5 приоритетов, а у одного их 20, то мы будем смотреть максимум до 20 приоритета этого единственного абитуриента, но важный момент, что уже начиная с 6 и по 20 приоритет мы будем запоминать только его, так как остальные после своего 5 приоритета просто выкидываются).
