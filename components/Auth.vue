<script setup>

const supabase = useSupabaseClient()

const loading = useState('loading', () => false)
const email = useState('email', () => '')

const handleLogin = async () => {
    try {
        loading.value = true
        console.log(email.value)
        const { error } = await supabase.auth.signIn({ email })
        if (error) throw error
        alert('Check your email for the login link!')
    } catch (error) {
        alert(error.error_description || error.message)
    } finally {
        loading.value = false
    }
}

const handleOnChange = (event) => {
    email.value = event.target.value
}
</script>

<template>
    <div className="row flex flex-center">
        <div className="col-6 form-widget">
            <h1 className="header">Supabase + Next.js</h1>
            <p className="description">Sign in via magic link with your email below</p>
            <div>
                <input className="inputField" type="email" placeholder="Your email" :value="email"
                    @change="handleOnChange" />
            </div>
            <div>
                <button @click="handleLogin" className="button block" :disabled="loading">
                    <span>{{ loading ? 'Loading' : 'Send magic link' }}</span>
                </button>
            </div>
        </div>
    </div>
</template>