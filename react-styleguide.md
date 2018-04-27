
## Styleguide for react components

- Использовать *`lodash`* только при работе c коллекциями

> import _ from 'lodash'

------------
- Использовать глобальные плагины такие как *`React, Redux, PropTypes и.т.д`*

> import React, { Component } from 'react'

> import PropTypes from 'prop-types'

------------
- Использовать общие компоненты *`ca-common`*

> import { CATable, CARow, CACell } from 'ca-common/ui-lib/components/TableElements'

------------
- Использовать *`fetcher`*

> import {fetchWrapper} from 'ca-common/redux/modules/common'

------------
- Использовать стили для компонента *`scss`*

> import './AccountActivity.cscc'

------------
- Использовать константы

> import { arrayValue } from './array'

------------
### Создание компонента через class

Компоненты на основе классов — это stateful компоненты (с внутренним состоянием). 
Использовать их надо только там где они нужны!

- Создание компонента через *`class`*

> class AccountActivity extends Component

------------
- Все статичное выводим тут в следующем порядке:

	- Статические методы и переменные:

		> 		static ARRAY = [1,2,4,5]
		> 		static METHOD() {}

	- Статические *`propTypes`* и *`defaultProps`*:

        > 		static propTypes = {
        > 			option: PropTypes.string,
        > 			age: PropTypes.number.isRequired
        > 		}

        > 		static defaultProps = {
        > 			option: 'Я принимаю строку поскольку я не isRequired'
        > 		}

	* ***Примечание***: описываем props типа объект в propTypes

        > 		static propTypes = {
        > 			letter: PropTypes.shape({
        > 				number: PropTypes.number
        > 			}).isRequired
        > 		}

------------
- Использовать *`constructor`*, если он необходим

* ***Примечание***: Обходимость возникает при использовании (state)
	> 		constructor(props) {
	> 			super(props);
	> 			this.state = {
	> 				checkValue: this.props.checking
	> 			}
	>		 }

* ***Примечание***: props в конструктор не пробрасываем, если мы не используем его через this.props

	> 		constructor() {
	> 			super();
	> 			this.state = {
	> 				checkValue: 'I am state'
	> 			}
	>		 }

------------
- Использование *`Lifecycle methods`* , если он необходим.

	> 		componentDidMount() {
	> 			this.timerId = setInterval( ()=> this.tick(), 1000 )
	> 		}

------------
- Использование методов класса, которые использует компонент при вызове событий

	> 		handleChechoxShowStatus = () => {
	> 			console.log('I am event method')
	> 		}

* ***Примечание***: Желательно использовать стрелочные функции `arrow function` и называть методы с суфиксом "*handle*"

------------
-  Использование метода *`render`*

* ***Примечание***: В методе *`render`* используйте деструктуризацию пропросов и стейтов

	>		const {checkboxStatus, accout} = this.props
	> 		const {checkValue} = this.state

------------
- Использование метода *`return`*

* ***Примечание***: Стараемся избегать анонимных функций в методе render. Выносите их в отдельные функции

	> 		return (
	> 			<CACheckbox checkboxStatus={this.handleCheckboxStatus} />
	> 		)

------------
- Использование метода *`mapStateToProps`*

* ***Примечание***: Если нам необходимо вытянуть данные из (store) используем mapStateToProps

	> 		function mapStateToProps (state) {
	>			return {
	> 				user: state.user
	>			}
	>		 }

------------
9. Использование метода *`mapDispatchToProps`*

* ***Примечание***: Чтобы сохранить некоторые сообщения, Redux предоставляет bindActionCreators(), который позволяет вам это сделать

	> 		function mapDispatchToProps(dispatch) {
	> 			return bindActionCreators({ increment, decrement }, dispatch);
	>		 }

------------
- Использование метода *`connect`*

* ***Примечание***: Функция *`connect`* позволяет нам получить в качестве props для компонента данные из store. *`mapStateToProps`* и *`mapDispatchToProps`* передаем по мере необходимости

	> connect(mapStateToProps, mapDispatchToProps)(AccountActivity)

------------

### Stateless functional components

* ***Пример***

	> 		const Square = ({ value, onClick }) => { 
	> 			<button className="square" onClick={onClick}>{value}<button/>
	>		 )}

------------
