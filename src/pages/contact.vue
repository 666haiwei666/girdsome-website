<template>
    <Layout>
        <!-- Page Header -->
        <header class="masthead">
            <div class="overlay"></div>
            <div class="container">
                <div class="row">
                    <div class="col-lg-8 col-md-10 mx-auto">
                        <div class="page-heading">
                            <h1>Say hi!</h1>
                            <span class="subheading">Leave me a note with any questions you might have, I'll get back to
                                you as soon as possible.</span>
                        </div>
                    </div>
                </div>
            </div>
        </header>

        <!-- Main Content -->
        <div class="container">
            <div class="row">
                <div class="col-lg-8 col-md-10 mx-auto">
                    <p>Want to get in touch? Fill out the form below to send me a message and I will get back to you as
                        soon as possible!</p>
                    <form name="sentMessage" id="contactForm" @submit.prevent="onSubmit">
                        <div class="control-group">
                            <div class="form-group floating-label-form-group controls">
                                <label>Name</label>
                                <input v-model='form.name' type="text" class="form-control" placeholder="Name" id="name"
                                    required data-validation-required-message="Please enter your name.">
                                <p class="help-block text-danger"></p>
                            </div>
                        </div>
                        <div class="control-group">
                            <div class="form-group floating-label-form-group controls">
                                <label>Email Address</label>
                                <input v-model='form.email' type="email" class="form-control"
                                    placeholder="Email Address" id="email" required
                                    data-validation-required-message="Please enter your email address.">
                                <p class="help-block text-danger"></p>
                            </div>
                        </div>
                        <div class="control-group">
                            <div class="form-group floating-label-form-group controls">
                                <label>Message</label>
                                <textarea v-model='form.message' rows="5" class="form-control" placeholder="Message"
                                    id="message" required
                                    data-validation-required-message="Please enter a message."></textarea>
                                <p class="help-block text-danger"></p>
                            </div>
                        </div>
                        <br>
                        <div id="success"></div>
                        <button type="submit" class="btn btn-primary" id="sendMessageButton">Submit form</button>
                    </form>
                </div>
            </div>
        </div>
    </Layout>
</template>

<script>
    import axios from 'axios'
    export default {
        name: 'ContactPage',
        data() {
            return {
                form: {
                    name: '',
                    email: '',
                    message: ''
                }
            }
        },
        methods: {
            async onSubmit() {
                try {
                    let res = await axios({
                        method: 'post',
                        url: process.env.GRIDSOME_API_URL + `/Contacts`,
                        data: this.form
                    })
                    window.alert('提交成功')
                    this.$router.replace('/')
                } catch (error) {
                    window.alert('发送失败')

                }
            }
        }
    }
</script>

<style>
    input,
    textarea {
        background: transparent;
        border: 1px solid #cccccc;
        outline: none;
        border-radius: .3rem;
        padding: .8rem 1rem;
        color: inherit;
        font-size: 1rem;
        width: 100%;
        margin-top: 20px;
    }

    button {
        color: #ffffff;
        background: #333333;
        outline: none;
        border: 0;
        font-size: .8rem;
        padding: .8rem 1.6rem;
        border-radius: .3rem;
        margin-top: 2rem;
        cursor: pointer;
        transition: opacity .25s ease;
        font-size: 500;
        letter-spacing: .035em;
    }
</style>